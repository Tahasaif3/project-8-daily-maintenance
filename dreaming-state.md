# Dreaming Loop - State

last_reviewed_entry_date: 2026-08-15

## Proposals made

### 2026-09-21 review
`progress.md` on `main` has no `## Entries` dated after 2026-08-15, same
as at the last review, so a literal read of the spine alone would say
"nothing to review." But every daily-digest/dreaming-loop run since
2026-08-16 has instead been landing as its own unmerged branch/PR
against the same stale `main` (PRs #3-#40, none merged or closed since
PR #2 on 2026-08-15) - so the real run history lives across those PR
bodies, not in `main`'s `progress.md`. Checked that history via the
repo's PR list.

**Repeated failure found (2 occurrences, growing, same signature both
times):**
- PR #31 (`daily-digest/2026-09-11`, "Daily digest 2026-09-11: PR
  backlog is blocking the spine"): "`main` has not moved since PR #2
  merged on 2026-08-15. Every scheduled run since 2026-08-16 has opened
  a PR (24 daily-digest PRs... plus 4 dreaming-loop PRs...) and none of
  them have ever been merged. Because `main` never advances,
  `progress.md`'s `Last checked` pointer has stayed pinned to the
  2026-08-15 state, so every run since has re-derived the same single
  project-4-fix-loop commit as 'new' and opened a near-duplicate PR."
- PR #40 (`daily-digest/2026-09-20`, "...PR backlog still blocking
  spine"): identical diagnosis, backlog grown to "#3 through #39 - 37
  total," explicitly citing PR #31 as the first report. PR #40's own
  diff is itself another near-duplicate of PR #31's (same single
  `5528f97` README commit re-reported as "new").

Same root cause both times: nothing merges the PRs daily-digest/
dreaming-loop open, so `progress.md`'s `Last checked` values on `main`
never move, so every subsequent run re-derives the same stale diff and
piles on another near-duplicate open PR. Not a one-off - it recurred
identically nine days apart and was still unaddressed at the second
occurrence.

**Proposed fix (smallest found):** added a check to
`.claude/skills/daily-digest/SKILL.md` step 1 - at the start of each
run, check this repo's own open PRs for unmerged daily-digest/
dreaming-loop runs, and if a backlog exists, say so explicitly in
today's entry. This was already being done ad hoc by whichever run
happened to notice (PR #31, then PR #40 citing #31) - the fix makes it
a required check every run, not something that depends on the acting
run happening to look. It does not attempt to auto-close or auto-merge
anything; only a human can actually clear the backlog (per this loop's
own PR-not-direct-commit rule), and PR #40 already recommends that
action to the human reviewer.

**Rule deletion:** none proposed. All six steps of daily-digest
SKILL.md (read spine, gather w/ retry, draft, check draft, write
quiet/new, stop-without-writing on unclean failure) are still exercised
by the run history in the open PRs (e.g. step 4's draft-vs-raw-data
check is explicitly invoked in both PR #31 and PR #40's bodies). Step
6's stop-without-writing safety net still hasn't fired in any reviewed
PR, but as the 2026-08-15 review already noted, "hasn't fired yet" is
not the same as "unneeded."

`last_reviewed_entry_date` is advanced to 2026-09-20 (the most recent
dated run reviewed, PR #40), not left at 2026-08-15 - the entries were
found and reviewed via the PR backlog, so the review did cover real
run history through that date even though none of it has reached
`main`'s `progress.md` yet.

Flagged for a human, not a SKILL.md matter: the backlog itself (PRs
#3-#40) needs a human to merge one and close the duplicates - no rule
change fixes the fact that nothing has merged since 2026-08-15.

### 2026-08-15 review
Reviewed all progress.md entries (2026-08-09 through 2026-08-15, first
review since state was `none`).

Repeated failure found: `project-5-codify-body` gathering failed with a
`gh api` 403 rate-limit error right after listing commits, on
2026-08-10, 2026-08-12, and 2026-08-14 (3 occurrences, identical
signature, always handled by skipping the repo with no retry). Proposed
fix: added a single 60s-wait-and-retry to daily-digest SKILL.md step 2
before falling back to the existing skip-and-continue behavior.

One-off, not proposed as a rule change: 2026-08-14 NOTES.md commit had
a typo ("mainatenance"); happened exactly once, no pattern.

Rule deletion: none proposed. Every rule in daily-digest SKILL.md
(read spine, gather, draft, check draft, write quiet/new, stop-without-
writing on unclean failure) was load-bearing across the reviewed
period - including step 6's stop-without-writing path, which is the
safety net for total gathering failure or a malformed spine and simply
hasn't fired yet, not a rule that's unneeded.
