# Daily Digest

Dated entries land here whenever the daily-digest run finds something
new across the watched repos. Quiet days are logged in `progress.md`
instead, not here - see that file for the full run history.

## 2026-08-15 (first run)

**project-4-fix-loop**
- New repo, 2 commits on `main`: "add cart discount tool (tier boundary bug)"
  then "record PASS/FAIL results in README".
- PR #1 open, "Fix discount tier boundaries (off-by-one)": changes the
  `quantity > 10` / `quantity > 5` checks to `>=` so exact-boundary
  quantities (5 and 10) get the discount tier they should. PR body records
  an independent reviewer verdict of PASS and all 3 tests passing. Not
  merged yet.
- No issues.

**project-5-codify-body**
- New repo, 9 commits on `main`. Scaffolded with three buggy candidates
  plus the codify-body skill, then worked through them:
  - `word_count` fixed to collapse extra whitespace - reviewer PASS, merged.
  - `fahrenheit_to_celsius` fixed (was using 30 instead of 32 in the formula).
  - discount percent capped at 100 - reviewer PASS, merged.
  - a dedupe candidate was added (order-preserving bug), then fixed to
    preserve first-occurrence order.
  - README updated documenting run 1 and run 2 results.
- No open PRs (this repo merges straight to `main` via "merge: ... (reviewer
  PASS)" commits rather than PRs). No issues.

**project-6-doorbell-loop**
- New repo, 2 commits on `main`: "add queue_position with bounds check +
  tests" then "document doorbell loop results".
- PR #1 open, "Simplify next_in_line" (branch `bug/remove-bounds-check`):
  first commit removed the bounds check, a second commit 8 minutes later
  ("restore bounds check") put it back. Net diff against `main` is now
  empty - no files changed. Not merged.
- No issues.

## 2026-09-12

**project-4-fix-loop**
- One new commit on `main`: "Update README.md" (5528f97), on top of the
  last-checked commit. One-line copyedit only - removes a trailing period
  from the last line of the fix-summary table, no functional change.
- PR #1 ("Fix discount tier boundaries (off-by-one)") unchanged: still
  open, not merged.
- No issues.

**project-5-codify-body**
- No new activity. `main` is still at the last-checked commit, no new
  PRs or issues.

**project-6-doorbell-loop**
- No new activity. `main` is still at the last-checked commit, PR #1
  ("Simplify next_in_line") unchanged and still open.
- No issues.
