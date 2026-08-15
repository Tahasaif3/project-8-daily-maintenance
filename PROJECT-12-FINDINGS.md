# Project 12 - The Dreaming Loop (Capstone 2)

Idea: a second loop, on a weekly schedule, that reads Project 8's own run
history and asks one question - did the same problem happen more than
once? If so, propose the smallest rule fix, as a PR, never a direct
commit. Built on top of Project 8, not a separate repo - it reads and
proposes changes to the same `daily-digest` skill it's watching over.

## A note on the test data
Project 8 only started running for real on 2026-08-15 - one real entry
isn't enough to prove a "repeats vs. one-off" detector actually works.
So `progress.md` was backfilled by hand with six days of plausible
history (2026-08-09 through 2026-08-14): a `gh api` 403 rate-limit
failure on `project-5-codify-body`, in the exact same spot, three
separate times, plus one unrelated one-off typo. This is disclosed here
plainly - the entries are simulated, not real runs, and exist only to
give the dreaming-loop something real to catch.

## What happened
Fired the weekly routine once as a test run. It:
- Read `dreaming-state.md` (`last_reviewed_entry_date: none`) and all of
  `progress.md`'s entries.
- Correctly identified the repeated failure: same `gh api` 403, same
  point in the run, same repo, on three different dates - and quoted
  each entry verbatim as evidence in the PR body.
- Correctly did **not** treat the one-off NOTES.md typo (2026-08-14) as a
  pattern - it happened once, so no rule was proposed for it.
- Proposed the smallest fix: a single 60-second wait-and-retry before
  falling back to the existing skip behavior.
- Reviewed every rule in `daily-digest/SKILL.md` for a deletion
  candidate and found none - said so explicitly instead of forcing one
  just to fill the checklist item.
- Committed both changes (`SKILL.md` fix + updated `dreaming-state.md`)
  on branch `claude/zen-mayer-qn3ztn`, never touched `main` directly, and
  opened **PR #2**: https://github.com/Tahasaif3/project-8-daily-maintenance/pull/2

Verified independently (not just trusting the routine's own summary): read the actual PR body via `gh pr view` - every claim in it traces to a real, quoted `progress.md` entry.

## Done when - checked against the actual assignment criteria
- **The PR's proposed change traces to real, cited log entries, not a
  guess.** Yes - three dated entries quoted verbatim in the PR body.
- **A deliberately planted repeated failure gets caught and turned into
  a proposal.** Yes - the 3x rate-limit pattern, caught precisely.
- **Nothing changed without a human merging it.** Yes - PR #2 sat open,
  unmerged, until reviewed by hand and merged on 2026-08-15 at 07:12 UTC.
  `main` only picked up the retry fix because that review happened -
  the loop itself never had merge access.

## After merge
`main` now runs the retry-once fix. The next real weekly fire (17 Aug)
starts from `last_reviewed_entry_date: 2026-08-15` - it will only see
whatever repeats after that point, not the pattern that's already fixed.

## The one honest failure mode this proves it avoids
An improvement loop that always finds something to propose - whether or
not anything actually repeated - is worse than one that sometimes does
nothing, because its guesses steer every future run. This run had a real
deletion candidate available to "find" if it wanted to look busy (the
step-6 safety net that hadn't fired yet). It didn't take the bait -
it reasoned that "hasn't fired yet" isn't the same as "unneeded," and
said so.
