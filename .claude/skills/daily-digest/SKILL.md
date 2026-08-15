---
name: daily-digest
description: The daily maintenance chore, written down once. Checks three watched repos for anything new since last time, drafts a digest, checks its own draft against the raw data before writing anything, and updates the spine either way.
---

# daily-digest

The chore: every morning, look across three practice repos for anything
that happened since yesterday, and keep a running log. Boring on
purpose - that's what makes it a real test of the loop staying honest
over many unattended runs, not a one-off demo.

## Steps

1. **Read the spine.** Open `progress.md`. For each watched repo, read
   its `Last checked` value (a commit SHA, PR/issue number high-water
   mark, or `none` on the very first run).

2. **Gather, per repo.** Using `gh api` / `gh pr list` / `gh issue list`
   / `git log`, find anything new since the last-checked point: commits,
   opened or merged PRs, opened or closed issues. If a repo shows
   `none`, this is its first check - gather everything currently there,
   not just "recent" activity.

3. **Draft (implementer).** Write a short digest: what changed, per
   repo, in plain sentences. If a repo had nothing new, say so plainly
   instead of padding the digest with filler.

4. **Check the draft (reviewer).** Before writing anything, re-derive
   the facts independently from the raw `gh`/`git` output gathered in
   step 2 and compare against the draft line by line. Every claim in the
   digest must trace back to something actually observed in step 2 - not
   remembered from a previous run, not inferred, not guessed. Cut
   anything that doesn't check out.

5. **Write, only if the check passes.**
   - If nothing new was found anywhere: append a short "quiet day" entry
     to `progress.md`. Do not touch `NOTES.md` - a commit for "nothing
     happened" is noise.
   - If something new was found: append the dated digest to `NOTES.md`,
     commit and push directly to `main` (the review in step 4 is the
     gate - nothing reaches `NOTES.md` without passing it).
   - Either way, update each watched repo's `Last checked` value in
     `progress.md` to what was just gathered, so tomorrow's run starts
     from today, not from scratch.

6. **If step 2 or 4 can't be completed cleanly** (a repo is unreachable,
   the draft can't be verified against the data, the spine itself looks
   malformed) - stop without writing anything, and leave a note in
   `progress.md` under today's date saying exactly what blocked the run.
   Guessing and continuing is worse than an honest gap in the log.
