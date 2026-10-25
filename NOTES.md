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

## 2026-10-25

**project-4-fix-loop**
- `main` was replaced. It is now one parentless commit, 5528f97 "Update README.md"
  (Taha Saif, 2026-08-16). The previous tip, 43bf5a5 "record PASS/FAIL results
  in README", is no longer on any branch.
- The new `main` matches 43bf5a5 except README.md's last line lost its trailing
  period. `cart_total.py` on `main` still has the `>` tier bug.
- Branches `fix/discount-boundaries` (c89bfee) and `fix/discount-boundaries-bad`
  (e1c1a3a) are unchanged, and PR #1's head is still c89bfee. PR state
  (open/merged) not checked, see `progress.md`.

**project-5-codify-body**
- Nothing new. `main` is still 2654519 and there are no other branches.

**project-6-doorbell-loop**
- Nothing new. `main` is still 4d4a2a2. `bug/remove-bounds-check` and PR #1's
  head are still 3735e33, with the same README-only diff against `main`.
  PR state not checked.
