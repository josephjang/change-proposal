# Pattern: before-after

Describes what changed, how it worked before and why, how it works after, and where, for readers who will not open the diff: a colleague a year later, an agent searching the area, a reviewer of a superseding proposal.

**When.** Proposals are read without their pull request (months later, by agents, across repositories) and readers cannot reconstruct what actually changed. Or the reason something was built the old way is lost because the diff shows only "after".

**Goes with.** `human-ai-split` (this is the section an assistant drafts best), `agent-context` (agents read it to locate the change), `supersession` (a superseding proposal says what "before" it undoes).

## What it adds

**One section**, placed after `Requirements`:

```
## Change
- Before: (how it works today, and why it was built that way)
- After: (what changes, as behavior, not as code)
- Where: (paths of the modules or files that change)
Flow: input → state → output, in one line
```

The "Before" line is the part the diff cannot supply. The guide's `Problem` section may already have put it there, in which case the line points there.

## Using it

- "Where" is paths, not copied code.
- "Before" includes why the previous behavior was the way it was, when that is known. An inference is marked as one; a confident-sounding guess about the past is worse than no line.

## Cost

Four lines, mostly derivable from the diff.

## Removing it

Drop the section from the template. Existing proposals keep it.
