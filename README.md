# Project 8 - Your Own Daily Loop (Capstone)

A real, boring, recurring chore: every morning, check three of my other
practice repos (Project 4, 5, 6) for anything new, and keep a running
log. Meant to run unattended, for real, not just demoed once.

## The six parts, all in this one repo

1. **Heartbeat** - a Claude routine on a daily schedule (not an event
   this time, unlike Project 6 - a genuinely different heartbeat kind).
   No prompt typed by hand each morning.
2. **Worktree** - each routine run gets its own fresh sandboxed
   checkout, so one day's run can never collide with another's.
3. **Skill** - `.claude/skills/daily-digest/SKILL.md` holds the exact
   steps once. Every run reads it instead of re-deriving what "check
   the repos" means from scratch.
4. **Maker-checker** - the run drafts a digest, then re-derives the same
   facts independently from raw `gh`/`git` output and checks the draft
   against them line by line before writing anything. Nothing gets
   committed on a claim that doesn't trace back to real data.
5. **Connector** - the run can act: commits `NOTES.md` and pushes to
   `main` for real. Not a suggestion in a chat window - an actual write.
6. **The spine** - `progress.md` tracks a `Last checked` point per
   watched repo plus a dated entry every run, quiet or not, so day 5
   visibly builds on day 1 instead of re-scanning everything from
   scratch each morning.

## Watched repos
- Tahasaif3/project-4-fix-loop
- Tahasaif3/project-5-codify-body
- Tahasaif3/project-6-doorbell-loop

## Done when
- It has run unattended for a week - not a one-time demo, actual daily
  fires with no one pasting a prompt in.
- The changes it ships (`NOTES.md` entries) are trusted because they
  were checked against real data each time, not because nobody looked.
- Concept 15, honestly: did my understanding of what this loop is doing
  keep up with what it's actually changing? See `REFLECTION.md`.
