# Daily Digest

Dated entries land here whenever the daily-digest run finds something
new across the watched repos. Quiet days are logged in `progress.md`
instead, not here - see that file for the full run history.

## 2026-09-19

**project-4-fix-loop**
- One commit since the spine's last-checked point (`43bf5a5`): `5528f97`
  "Update README.md" (2026-08-16), drops a trailing period in the
  fix-loop write-up. No functional change. PR #1 ("Fix discount tier
  boundaries (off-by-one)") still open, unchanged since 2026-08-14.

**project-5-codify-body**
- Nothing new: no commits, PRs, or issues since the spine's last-checked
  point (`2654519`).

**project-6-doorbell-loop**
- Nothing new: no commits since the spine's last-checked point
  (`4d4a2a2`). PR #1 ("Simplify next_in_line") still open, unchanged
  since 2026-08-14.

**The actual finding, again**
`main` in this repo has not advanced past PR #2 (merged 2026-08-15).
36 daily-digest/dreaming-loop PRs (#3-#38) are open and unmerged, going
back to 2026-08-16. Because `main` never moves, `progress.md`'s
`Last checked` pointer has stayed pinned to the 2026-08-15 state, so
every run since - including this one - re-derives the same single
project-4-fix-loop commit as "new" and opens a near-duplicate PR. PR #31
(2026-09-11) already flagged this exact problem 8 days ago; it is still
unresolved 34 days after main last moved. This PR is functionally a
duplicate of #31 and #38.

**Recommend:** merge one open digest PR (this one, or #38) and close the
rest of the backlog as duplicates so `progress.md`'s spine can actually
advance. The `dreaming-loop` PR backlog (#4, #10, #18, #26, #34) likely
needs the same cleanup.

Draft verified line-by-line against `git compare` output and the
GitHub API (commits, PRs, issues) for each watched repo, and against the
open-PR list for this repo, before writing (step 4 of the daily-digest
skill).

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
