# Dreaming Loop - State

last_reviewed_entry_date: 2026-11-23

## Proposals made

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

### 2026-11-16 review
`main`'s `progress.md` still ends at 2026-08-15, but that is not because
nothing ran: 82 daily-digest branches (2026-08-16 through 2026-11-16,
under five naming schemes) each carry an unmerged `progress.md` entry.
This review read all of them. The 11 earlier weekly reviews (2026-08-17
through 2026-11-09, also unmerged) read only `main` and each reported
"no new entries"; the 2026-08-31 one concluded no runs had happened.

Repeated failures found:

1. **Stale spine - the same commit re-reported every run.** Every entry
   from 2026-08-17 through 2026-11-16 reports project-4-fix-loop commit
   `5528f97` ("Update README.md", 2026-08-16) as new, because each run's
   `Last checked` update sits on an unmerged branch and the next run
   reads `main`'s spine (still `43bf5a5`). Flagged by the runs themselves
   on 2026-09-11 ("Every run since has been re-deriving the same 'new'
   commit against the same stale spine") and 2026-09-19/20.
   Fix (daily-digest step 1): read `Last checked` from the newest unmerged
   `daily-digest/<date>` branch when digest PRs are still open, and report
   the backlog count; step 5 fixes the branch name so it can be found.

2. **403 "access not enabled for this session" / GraphQL 403.** `gh api`
   returned 403 "GitHub access to this repository is not enabled for this
   session" on 2026-10-02, 10-03, 10-04, 10-05, 10-06, 10-09, 10-11,
   10-12, 10-23, 10-27, 10-28, 10-30, 11-05, 11-07, 11-10 (15 entries),
   and `gh pr list`/`gh issue list` returned a GraphQL 403 on 2026-10-07,
   10-13, 10-14, 10-23, 10-25, 10-29, 11-01, 11-03, 11-06, 11-08, 11-10,
   11-13, 11-15, 11-16 (14 entries). Eight runs were blocked outright
   (2026-10-05, 10-09, 10-12, 10-17, 10-28, 10-30, 11-01, 11-10). Runs
   that switched to REST `gh api` endpoints and/or attached the repo
   succeeded (e.g. 2026-11-16, 10-29). Several entries had to explain
   that the old rate-limit retry rule "does not apply".
   Fix (daily-digest step 2): use REST endpoints, not GraphQL; on the
   access 403, attach the repo read-only and retry once, else step 6.

3. **Dreaming loop blind to unmerged history.** The 11 reviews listed
   above. Fix (dreaming-loop step 2): also read `progress.md` entries on
   unmerged digest branches and report the backlog.

Rule deletion: removed the daily-digest step-2 "403 rate-limit -> wait
60s, retry once, then skip" rule. Its only evidence was the 2026-08-10/
12/14 entries, which PROJECT-12-FINDINGS.md discloses were hand-written
test data, not real runs. Across 82 real runs no rate-limit 403 occurred
(entries repeatedly note "no rate-limit errors"), and its skip-and-continue
clause contradicted step 6 (stop on unreachable repo). The new step-2
text covers the 403s that actually happen.

Not proposed: branch-name sprawl (five schemes) is handled by the
step-5 naming line above rather than a separate rule.

Action needed by a human, outside SKILL.md: none of PRs #3-#96
(daily-digest and dreaming-loop) has been merged - `main` has not moved
since 2026-08-15. Until they are merged or closed,
`main`'s spine stays at 2026-08-15.

### 2026-11-23 review
Reviewed the 7 daily-digest entries dated 2026-11-17 through 2026-11-23.
All are on unmerged branches (PRs #98-#104); `main` still ends at
2026-08-15 and no PR since #2 has been merged, including last week's
review (#97). This branch is built on top of #97's branch, so merging
this PR also lands #97's changes; #97 can then be closed.

Repeated failures found:

1. **False claims about run history.** 2026-11-19 and 2026-11-23 both
   say "First run since 2026-08-15"; 2026-11-22 says "There are no
   logged runs between 2026-08-15 and today". About 95 digest PRs were
   open at the time, so all three claims are false (3 of 7 entries).
   Step 4 says every claim must trace to observed data, but runs did not
   treat statements about past runs as claims to check.
   Fix (daily-digest step 4): one sentence saying claims about earlier
   runs must be checked against open digest PRs, or left out.

2. **`gh pr list` / `gh issue list` tried first, 403, then REST.** All 7
   entries (2026-11-17 through 11-23) report a GraphQL 403 from
   `gh pr list`/`gh issue list`, then the same data fetched with REST
   `gh api`. #97 added the "use REST" paragraph, but step 2's first
   sentence still names `gh pr list` / `gh issue list` as the tools.
   Fix: see the rule deletion below.

3. **Branch name in #97 doesn't match what runs use.** #97 specifies
   `daily-digest/<date>`, and its step-1 stale-spine lookup searches for
   that name. 6 of the 7 runs this week used `claude/daily-digest-<date>`
   (11-17, 11-18, 11-20, 11-21, 11-22, 11-23); 11-19 used
   `digest/2026-11-19`. The `claude/` prefix is the one this environment
   lets runs push to. Fix: change both mentions to
   `claude/daily-digest-<date>`.

Still repeating, already addressed by #97 (unmerged): the stale spine.
All 7 entries re-report project-4-fix-loop `5528f97` (2026-08-16) as new.

Rule deletion: removed `gh pr list` / `gh issue list` from step 2's
list of gathering tools. They fail with a 403 on every run (7 of 7 this
week) and contradict the paragraph below them that says to use REST.

Action needed by a human, outside SKILL.md: PRs #3-#104 are all open.
Merge this PR (or #97), then merge or close the digest PRs. Until then
`main`'s spine stays at 2026-08-15 and every run re-reports `5528f97`.
