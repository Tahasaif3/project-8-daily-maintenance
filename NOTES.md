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

## 2026-11-05

**project-4-fix-loop**
- 1 new commit on `main`: `5528f97` "Update README.md" (2026-08-16, Taha
  Saif). One-line README change: removes the trailing period from the last
  line of the `fix/discount-boundaries-bad` note ("No PR opened for this
  branch"). Cosmetic only.
- Branches `fix/discount-boundaries` and `fix/discount-boundaries-bad`
  still exist; `refs/pull/1/head` is `c89bfee` (the `fix/discount-boundaries`
  tip).

**project-5-codify-body**
- Nothing new. `main` still at `2654519`.

**project-6-doorbell-loop**
- Nothing new. `main` still at `4d4a2a2`; `bug/remove-bounds-check` /
  `refs/pull/1/head` still at `3735e33`.

Caveat: the `gh` API was not usable this run (403 "GitHub access ... not
enabled for this session", not a rate limit), so this digest comes from
`git clone` / `git ls-remote` only. PR open/merged state, comments and
issues could not be checked.
