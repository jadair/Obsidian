# Decisions

How to make and record decisions in this vault. See [[00 Home/Working Methodology|Working Methodology]] for the broader principles and [[00 Home/Daily Workflow|Daily Workflow]] for the daily rhythm this fits into.

## Why Decisions Get Written Down

Decision-making is a distinct, structured act — not something that happens implicitly in conversation and gets left there. A real decision gets a record with context, options considered, and rationale, not just an outcome. If you can't write the rationale down in a few sentences, the decision probably hasn't actually been made yet.

This mirrors how effective operators at every level actually work: Amazon's written narrative memos and Andy Grove's insistence on explicit decision-forcing meetings both exist to stop decisions from staying implicit or getting relitigated because no one wrote down why a call was made.

## Where a Decision Record Goes

- **A decision made within a project** (a scoped, dated call with a rationale) → `Decision — Subject — YYYY-MM-DD.md` inside that project folder in `04 Projects/<Project Name>/`.
- **A cross-cutting decision** that doesn't belong to one project → `Decision — Subject — YYYY-MM-DD.md` in `05 Areas/` instead.
- Either way, start from the [[07 Templates/decision-record-template|decision record template]] so context, options considered, and rationale are captured consistently — not just the outcome.

## What Counts as a Decision Worth Recording

Not every choice needs a formal record. A decision is worth writing down when:

- It commits time, money, or people to one path over another.
- Reversing it later would be costly or disruptive.
- Someone is likely to ask "why did we do it this way?" months from now.
- It resolves a real disagreement or open question, not just a routine judgment call.

A one-line note in a daily note or meeting record is enough for small, easily-reversed choices. When in doubt, write the record — a record you didn't strictly need costs little; a real decision with no record costs you the ability to explain or revisit it later.

## Making the Decision

- **Name an owner.** "Someone should look at this" is not a decision or an action item. Match the task to whoever's strengths fit it, and reassign stalled items instead of letting them sit unowned.
- **Decide once, deliberately.** Don't let the same question get re-opened informally in every subsequent meeting — if new information genuinely changes the calculus, that's a new decision record that references and supersedes the old one, not a quiet reversal.
- **Capture it where it happened.** If a decision comes out of a meeting, log it in that meeting's `Decisions` section as it happens, then promote it to a full decision record afterward if it meets the bar above. Link the meeting record and the decision record to each other.

## Habits That Keep This Working

- **Write the decision down, not just the outcome.** A one-line "decided X" without the context and options considered isn't a decision record — it's a fact with no way to revisit whether it still holds.
- **Link decisions to what they affect** — the project, area, people, and any meeting they came out of — using `[[wikilinks]]` and frontmatter properties rather than duplicating context into the decision note.
- **Treat your daily notes and meeting records as the source of truth for how a decision came about**, not memory. When a decision record references "discussed with X," link to the actual meeting note.

## Related

- [[07 Templates/decision-record-template|Decision Record Template]]
- [[00 Home/Working Methodology|Working Methodology]]
- [[00 Home/Daily Workflow|Daily Workflow]]
- [[00 Home/Meeting Index|Meeting Index]]
