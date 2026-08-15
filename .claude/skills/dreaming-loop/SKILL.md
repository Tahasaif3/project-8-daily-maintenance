---
name: dreaming-loop
description: Weekly improvement loop over the daily-digest run history. Reads progress.md entries since the last review, finds failures or corrections that happened more than once, and proposes the smallest rule change that would prevent the repeat - as a PR, never a direct commit. Also proposes deleting one rule nothing recent needed.
---

# dreaming-loop

The daily-digest loop (Project 8) produces a dated entry every run,
quiet or not. This loop reads that history once a week and asks one
question: did the same problem happen more than once? If so, that's a
pattern worth writing down as a rule - not just noticed and forgotten
again next time it happens.

## Steps

1. **Read the state.** Open `dreaming-state.md`. Note
   `last_reviewed_entry_date` (a date, or `none` on the first run).

2. **Gather.** Read every entry in `progress.md`'s `## Entries` section
   dated after `last_reviewed_entry_date` (or all of them if `none`).

3. **Look for repeats, not one-offs.** Group entries by failure
   signature (same error, same point in the run, same repo). Anything
   that appears **more than once** is a candidate. A single one-off
   glitch is not - do not propose a rule change for something that
   happened exactly once.

4. **For each repeated pattern found:**
   - Draft the smallest possible addition to `.claude/skills/daily-digest/SKILL.md`
     that would prevent it recurring (a retry, a skip-and-continue
     instruction, a check to add - whatever is actually smallest).
   - The proposal must cite its evidence explicitly: which dated entries,
     how many times, and why this specific line stops it. No claim
     without a citation back to a real entry.

5. **Also propose one deletion.** Look at the current rules in
   `.claude/skills/daily-digest/SKILL.md`. If any rule wasn't needed by
   anything in the reviewed entries, propose removing it, with reasoning.
   If every rule was load-bearing, say so explicitly instead of forcing
   a deletion that isn't real.

6. **If no repeated pattern exists:** do not draft a change. Update
   `dreaming-state.md` and say plainly that nothing repeated this period.
   A dreaming loop that always finds something to change, whether or not
   anything actually repeated, is worse than one that sometimes does
   nothing.

7. **Write it up, always as a PR.**
   - Commit the proposed `SKILL.md` change (and the deletion, if any) on
     a new `claude/` branch.
   - Update `dreaming-state.md`'s `last_reviewed_entry_date` to the most
     recent entry reviewed, and log the proposal (or "nothing repeated")
     under `## Proposals made`, on that same branch.
   - Open a PR. Never commit any of this directly to `main` - a human
     reads and merges it, or it doesn't happen.
