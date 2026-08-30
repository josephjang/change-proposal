# Pattern: before-after

- **Requires**: core
- **Combines with**: `human-ai-split` (this is the section an assistant drafts best), `agent-context` (agents read it to locate the change), `supersession` (a superseding proposal says what "before" it undoes)
- **Conflicts with**: —

## Intent

Describe what changed — how it worked before and why, how it works after, and where — for readers who will not open the diff: a colleague a year later, an agent searching the area, a reviewer of a superseding proposal.

## Signal

Proposals are read without their pull request (months later, by agents, across repositories) and readers cannot reconstruct what actually changed. Or the reason something was built the old way is lost because the diff shows only "after".

## Adds

**One section**, placed after `Non-goals` (or `Goals / Non-goals`):

```
## Change
- Before: (how it works today, and why it was built that way)
- After: (what changes, as behavior — not as code)
- Where: (paths of the modules or files that change)
Flow: input → state → output, in one line
```

The "Before" line is the part the diff cannot supply; it is where the core's Problem section may already have put it, in which case the line points there.

## Rules

| ID | Rule | Principle |
|---|---|---|
| **BA1** | `Change` MUST state before, after and where. "Where" MUST be paths, not copied code. | P2 |
| **BA2** | "Before" MUST include why the previous behavior was the way it was, when that is known; an inference MUST be marked as one. | P2 |

## Cost

Four lines, mostly derivable from the diff.

## Remove

Drop the section from the template. Existing proposals keep it.
