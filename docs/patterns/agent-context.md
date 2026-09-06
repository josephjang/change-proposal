# Pattern: agent-context

**Candidate.** Written before anyone met its situation; not validated. It may be validated by use, absorbed into the core, or dropped. See [the catalog](README.md).

Turns merged proposals into constraints that coding agents actually read before they touch the same area, so that rejected alternatives are not rebuilt and non-goals are not quietly reversed.

**When.** An agent, or a person new to the area, rebuilds an alternative a proposal rejected, or implements something a proposal listed as a non-goal.

**Needs.** `proposal-metadata` (for `touches` and `status`) and `supersession` (an agent needs a validity check that does not require reading history). Goes naturally with `human-ai-split` (the same instruction block carries its rules), `decision-promotion` (records are constraints too), `living-docs-bridge` (the instruction file is a living document) and `agent-skills` (skills automate the search).

## What it adds

**An instruction block** in the repository's agent file (`AGENTS.md`, `CLAUDE.md`, or the tool's equivalent):

> **Change proposals.** This repository records the intent and judgment behind changes in `docs/changes/`; the patterns in use are stated at the top of `docs/changes/README.md`.
> **Before changing code**: search `docs/changes/` for proposals whose `touches` overlap the area you will touch (or whose `Change` section names the paths). For every proposal with `status: implemented`, treat `Decisions` (split or not), `Non-Goals` and `Risks` as constraints. If your task would reverse one, say so before writing code. Treat `superseded` and `abandoned` proposals as history; follow `superseded_by`. If `docs/decisions/` exists, `accepted` records there are constraints too.
> **While building**: if the proposal has `Requirements`, they are your stopping condition.
> **When finishing**: follow the drafting rules of `human-ai-split` and `evidence-verification` if this repository uses them (see `docs/changes/README.md`). Never edit a proposal whose status is `implemented` or `superseded`.

**A reading of `status`.** `implemented` is a constraint; `accepted` is a constraint on design; `draft` is context only; `superseded` and `abandoned` are history.

**A controlled `touches` vocabulary**, declared in `docs/changes/README.md` once the repository holds more than about thirty proposals, so that search hits reliably.

## Using it

- The instruction file has to exist and carry the block. An agent that is never told to look will not look.
- An agent that would have to violate a constraint tells the person first, before writing code. That conversation is the point of the pattern.
- Keep `touches` meaningful. Free-form tags work for a while; past a few dozen proposals, a declared vocabulary is what keeps the search honest.

## Cost

A few lines in the instruction file, one search per change, and keeping `touches` meaningful.

## Removing it

Delete the block. Agents treat the repository as code only.
