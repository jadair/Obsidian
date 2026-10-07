Nothing has been deleted; this is a read-only report. I pruned remote-tracking refs, then checked each worktree for uncommitted changes and each branch for merge status against `origin/develop` and for PR state.

## Worktrees (32 besides the main checkout)

**Safe to remove: clean, and the branch is merged, detached, or has a closed PR (18)**

|Worktree|Branch|Note|
|---|---|---|
|`~/.codex/worktrees/2cfc`, `3922`, `c864`, `eea4`|detached|Codex leftovers from March–April|
|`hotfix-16.29.2`|**`develop`**|It holds `develop`, so you can't check `develop` out anywhere else. Remove this first.|
|`hotfix-16.29.5`|hotfix/16.29.5|merged|
|`agent-a00523421a82cab32`|claude/issue-345-346-awards-queries|merged, remote gone|
|`agent-ac6703955aac8b8f3`|claude/issue-340-341-343-report-export-n1-v2|merged|
|`agent-acdc01f957cf7f376`|issue-337-work|merged|
|`django-ai-plugins-marketplace-b870a4`|detached||
|`issue-310-8a0ee8`|detached||
|`permissions-rules-inventory-274e90`|detached||
|`pr-370-feature-verify-fcb555`|claude/cranky-dewdney-0204fa|merged|
|`proposal-creation-error-6012d2`|hotfix/proposal-note-invisible-chars|PR #362 closed without merging|
|`vscode-worktree-visual-themes-1f7677`|claude/navbar-white-on-mui-v4-pages|merged, remote gone|
|`agent-a600cd0cfce35cf01`|claude/issue-327-328-ta-endpoint-authz|PR #374 **open**: remove the worktree, keep the branch|
|`agent-a839ad8be1a95f96a`|claude/issue-331-dept-head-scope|PR #371 **open**: remove the worktree, keep the branch|
|`agent-aab6529533391f23d`|claude/issue-326-ca-api-auth|PR #375 **open**: remove the worktree, keep the branch|
|`memory-usage-benchmark-76cc5e`|claude/issue-333-discord-duplicate-submit|PR #372 **open**: remove the worktree, keep the branch|
|`pr-362-review-468928`|fix/note-author-and-save-bugs|PR #369 **open**: remove the worktree, keep the branch|

**Clean, but the branch has commits that aren't merged and has no PR (2)**

- `ci-workflow-plan-3803f9` has feature/pin-npm-dependencies: 1 commit.
- `event-blackout-dates-csv-bc2eea` has feature/event-blackout-dates-csv: 4 commits.

**Uncommitted changes: look before removing (11)**

|Worktree|What's there|
|---|---|
|`~/.codex/worktrees/f54d` (codex/remove-debug-prints-237, merged)|**23 files changed (+695/−601)** in Scheduler React and templates. The biggest one.|
|`nostalgic-hypatia-fde40a`|Edits to `API/views.py` and `Scheduler/models.py`, plus a new migration `0033_dedupe_availability.py`|
|`quirky-kalam-43d8d0`|Edits to Scheduler views, tests and `view_employees`|
|`agent-a69f1c430723cfdc6`|Edits to proposal `views.py` and a new `test_search_team_filters.py`|
|`agent-ac434c6930f4f3446`|New `test_export_queries.py`|
|`agent-aa0c63cd58dac670f`|Edits to `ProposalTrackingSystem/home/tests.py`|
|`agent-acd4a9beb315d6763`|New `CourseAssistant/test_exploit_probe.py`, probably a security-review scratch file|
|`great-darwin-f4c3c3`|Edit to `pytest.ini`|
|`api-duplication-audit-6af942`|New `populate_userprofile_department.py` script|
|`scheduler-class-import-updates-4d1a7a`|New `CCIA/settings/reviewdev.py`|
|`hotfix-16.29.6`|Only new `.impeccable/` and `PRODUCT.md`, probably disposable|

## Branches with no worktree

**Merged into develop: safe to delete with `git branch -d` (~60)**

- **Agent leftovers:** the 9 `worktree-agent-*` branches.
- **Remote deleted:** `feature/create_classes_from_import`, `feature/import_updates`, `feature/CCIA-701`, `feature/CCIA-807`, `feature/CCIA-808`, `feature/accu-export`, `feature/#310`, `247-proposal-update-form…`, `claude/workflow-diagrams-docs-81834b`, `claude/issue-332-feature-1a4b59`.
- **Everything else in the merged list:** the old `feature/*` branches back to 2023, `release/16.29.0`, `hotfix/16.28.4`, `hotfix/16.29.6`, `chore/*`, and about 20 `claude/*` session branches.

**Duplicates of other branches: safe to delete**

- `pr370` is a local copy of claude/issue-325-travel-privesc (PR #370).
- `review/employee-applicant-admin-management` is a review copy of #316 and is 19 commits behind.

**PR closed without merging: probably superseded, but delete with `-D` only after a look**

- `feature/214-let-admins-reopen…` (#312)
- `hotfix/1366-minimal` (#367)
- `hotfix/proposal-latin1-1366` (#366)
- `sync-test` (#322)

**Experiment branches with no PR**

- `test-master-cherry`
- `claude/selective-develop-master-sync-e587ea`

**Commits that aren't merged and no PR: need your call**

- **Recent:**
    - `claude/event-request-form-feature-96918d`
    - `claude/reopen-user-forms-a5b3e3`
    - `claude/scheduler-admin-dashboard-ee3ede`
    - `claude/scheduler-import-skip-missing-instructor`
    - `feature/test-cleanup`
- **Old (2022 to early 2026):**
    - `feature/form-component`
    - `feature/ccia-611`
    - `feature/assign-course-assistant`
    - `feature/dashboard`
    - `feature/docs`
    - `feature/export-updates`
    - `feature/gemini_docs`
    - `feature/proposal-react`
    - `feature/query-performance-audit`
    - `feature/schedule_ui_cleanup`

**Keep (open PRs):** #316, #318, #323, #369, #370, #371, #372, #374 and #375.

The merge check can't see squash merges, so a few of the branches listed as not merged may already be in `develop`. Want me to run the cleanup? I'd remove the 18 safe worktrees and delete the merged and duplicate branches, and leave the rest for you to decide.