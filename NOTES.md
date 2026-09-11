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

## 2026-09-11

**Process note - read this first.** `main` in this repo has not moved
since PR #2 merged on 2026-08-15. Every scheduled run since then
(2026-08-16 through today) has opened a digest PR proposing content and
none of them - PRs #3 through #30, 24 daily-digest PRs plus 4 more from
the separate `dreaming-loop` skill (#4, #10, #18, #26) - has ever been
merged. Because `main` never advances, each run re-checks out the same
stale `progress.md` (`Last checked` still pinned to the 2026-08-15
state) and "discovers" the same single project-4-fix-loop commit below
as if it were new, every single day. This PR is functionally a duplicate
of at least PR #30 (2026-09-10), which found and reported the identical
facts. Recommend merging one of the open digest PRs (or this one) and
closing the rest of the backlog as duplicates so the spine can actually
advance; the `dreaming-loop` backlog likely needs the same treatment.

**project-4-fix-loop**
- 1 commit since the last state actually merged to `main` (`43bf5a5`):
  "Update README.md" (`5528f97`, 2026-08-16) - removed a stray trailing
  period at the end of the "No PR opened for this branch" sentence in the
  off-by-one bug notes. Wording only, no code change.
- PR #1 "Fix discount tier boundaries (off-by-one)" still open, unchanged
  since 2026-08-14.
- No issues.

**project-5-codify-body**
- Nothing new: no new commits, no PRs, no issues.

**project-6-doorbell-loop**
- Nothing new: no new commits. PR #1 "Simplify next_in_line" still open,
  unchanged since 2026-08-14. No issues.
