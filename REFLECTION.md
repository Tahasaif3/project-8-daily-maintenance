# Concept 15 - Did Understanding Keep Up?

Honest answer for run 1: mostly yes, with one real gap the loop itself
caught before I did.

## What I expected
Three quiet repos, a short "nothing much happened yet" digest, done in
under a minute.

## What actually happened
The run took 100 seconds and turned up something I hadn't tracked myself:
PR #1 on `project-6-doorbell-loop` still says "Simplify next_in_line" and
still shows as open, but its net diff against `main` is now empty - the
bug-then-fix commits canceled out. I knew this had happened (I made both
commits, in this same session, hours earlier) but I hadn't noticed the PR
itself was left in a stale, slightly misleading state. The digest caught
it because it checked the *current* diff against `main`, not what the
commits individually said they did.

## Where the loop diverged from what I told it
The skill said "push directly to main." The routine's own environment
pushed to a branch instead and left main untouched, because the sandbox
enforces its own branch-safety default regardless of what the prompt
says. I hadn't accounted for that when writing the skill. Rather than
fighting the platform's default, I changed the skill to match it -
branch, push, open a PR - which is arguably the more honest design
anyway: a PR is a second visible gate before anything lands, on top of
the draft-verify step already inside the run.

## The honest test
Understanding kept up here because I read the actual run log line by
line before writing this file, instead of trusting the routine's own
one-paragraph summary. If a future run's digest claims something and I
just skim the summary and move on, that's the moment this loop stops
being trustworthy - not because the loop got worse, but because I
stopped checking.
