	![[Pasted image 20260911103627.png]]

![[Pasted image 20260911103640.png]]



### Step 1 — Make the sample text submittable

**Goal:** the exact text you gave me saves through the form. Nothing else changes.

**What it is:** three `ALTER TABLE` statements. No code change, no Django migration, no app restart, no deploy. Django doesn't model column charset, so `makemigrations` stays silent (verified against an unreachable DB host — the autodetector never connects).

**1a. Back up.**

mysqldump --single-transaction --routines --triggers CCIA > ccia_pre_utf8mb4_$(date +%F).sql

**1b. Gate on the mojibake check — must return 0.** If any row is non-zero, stop: that data is double-encoded and conversion would corrupt it permanently. Returns 0 on the local copy.

SELECT COUNT(*) FROM proposal_notefield WHERE BINARY detail LIKE BINARY '%Ã%' OR BINARY detail LIKE BINARY '%â€%';

**1c. Convert.** Measured at 56ms / 114ms / 28ms on real copies of your data.

ALTER TABLE proposal_notefield CONVERT TO CHARACTER SET utf8mb4 COLLATE utf8mb4_0900_ai_ci;
ALTER TABLE proposal_proposal  CONVERT TO CHARACTER SET utf8mb4 COLLATE utf8mb4_0900_ai_ci;
ALTER TABLE awards_award       CONVERT TO CHARACTER SET utf8mb4 COLLATE utf8mb4_0900_ai_ci;

**1d. Verify — expect zero rows:**

SELECT TABLE_NAME, COLUMN_NAME, CHARACTER_SET_NAME FROM information_schema.COLUMNS
 WHERE TABLE_SCHEMA=DATABASE() AND CHARACTER_SET_NAME IS NOT NULL
   AND CHARACTER_SET_NAME <> 'utf8mb4'
   AND TABLE_NAME IN ('proposal_notefield','proposal_proposal','awards_award');

**1e. Prove it with your actual text** — submit the real form in the app, and/or round-trip it through the ORM in a shell to confirm before touching the UI.

**Rollback:** restore the dump. Converting back to latin1 is only safe before new 4-byte data is written.

**Why all three tables, not just notes:** the same request also writes `title`, `project_description`, and `equipment_desc` on `proposal_proposal`. Converting only `proposal_notefield` would move the error rather than remove it.

### Step 2 — Connection charset (needed for emoji)

Step 1 fixes your sample completely. It does **not** fix 4-byte characters (emoji), because those can't cross the current `utf8mb3` connection even into a `utf8mb4` column — I verified that directly.

One edit in CCIA/settings/base.py:17 (`DATABASES` is defined once; `production.py` doesn't override it):

'OPTIONS': {'charset': 'utf8mb4'},
'TEST': {'CHARSET': 'utf8mb4', 'COLLATION': 'utf8mb4_0900_ai_ci'},

The `TEST` change matters independently: your test DB is currently `utf8`, which is why no test caught this. Requires a deploy + restart. Small PR, no migration.

### Step 3 — The four real bugs

All in the lines around the crash, all independent of encoding. One small PR:

1. **`name=request.user.get_full_name`** — missing parentheses. Stores `"<bound method User.get_full_name of <User: ey86>>"` instead of the author's name. **This is live: 1,198 of 3,416 notes (35%) are affected.**
2. **`detail=str(notes)`** — stringifies the parsed JSON payload, persisting a Python repr as a user-visible note.
3. **`if note != ''`** — passes when `proNotes` is absent (`None != ''`), creating notes with `detail=None`.
4. **`award.save`** in awards/views.py:282 — missing parentheses, so the award is never saved after attaching a note.

Bugs 1 and 4 are the same mistake twice; worth a quick grep for other bare method references while you're in there.

### Step 4 — Repair the 1,198 note names

A one-off data migration or management command. **All 1,198 are fully recoverable** — the `owner_id` FK is intact on every row, so the repair reads `owner.get_full_name()` directly and ignores the broken repr entirely. No parsing, no guesswork.

Do this _after_ step 3, so the bug isn't still writing new bad rows while you clean up. Handle the edge case where `get_full_name()` is blank (falls back to username).

### Step 5 — Cleanup

- **Close [#367](https://github.com/CCISDG/CCIA/pull/367) and [#364](https://github.com/CCISDG/CCIA/pull/364).** Both are superseded. Leaving [#367](https://github.com/CCISDG/CCIA/pull/367) merged would be actively harmful once columns are `utf8mb4` — its sanitizer would keep stripping characters the database can now store.
- **Update [#365](https://github.com/CCISDG/CCIA/issues/365)** to cover the remaining 33 latin1 tables, and record that `django_cas_ng_proxygrantingticket` **cannot** be converted: its `session_key` is `varchar(1024)` = 4096 bytes in utf8mb4, over InnoDB's 3072-byte index limit. I tested it — it fails with error 3886. It's empty, third-party, and ASCII-only, so leave it.

### Sequencing

Step 1 is independent and ships today with no deploy. Steps 2–4 are one or two small PRs on `develop` through your normal release path. Step 5 is housekeeping.

One caveat to carry into production: all my measurements are against your local database. Confirm the row counts and the mojibake gate there before running step 1 — and if the production app user lacks `ALTER`, this needs whoever administers that database.

Want me to start on step 1, or prepare the step 3 + 4 PR first since that one goes through review anyway?