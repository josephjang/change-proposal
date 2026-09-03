# Pattern: agent-context

- **Requires**: core, `proposal-metadata` (for `touches` and `status`), `supersession` (agents need a validity check that does not require history)
- **Combines with**: `human-ai-split` (the same instruction block carries its rules), `decision-promotion` (records are constraints too), `living-docs-bridge` (the instruction file is a living document), `agent-skills` (skills automate the search)
- **Conflicts with**: editing merged proposals in place

## Intent

Turn merged proposals into constraints that coding agents actually read before they touch the same area, so rejected alternatives are not rebuilt and non-goals are not quietly reversed.

## Signal

An agent — or a person new to the area — rebuilds an alternative a proposal rejected, or implements something a proposal listed as a non-goal.

## Adds

**An instruction block** in the repository's agent file (`AGENTS.md`, `CLAUDE.md`, or the tool's equivalent):

> **Change proposals.** This repository records the judgment behind changes in `docs/changes/`; the composition in force is stated at the top of `docs/changes/README.md`.
> **Before changing code**: search `docs/changes/` for proposals whose `touches` overlap the area you will touch (or whose `Change` section names the paths). For every proposal with `status: implemented`, treat `Decisions` (split or not), `Non-Goals` and `Risks` as constraints. If your task would reverse one, say so before writing code. Treat `superseded` and `abandoned` proposals as history; follow `superseded_by`. If `docs/decisions/` exists, `accepted` records there are constraints too.
> **While building**: if the proposal has `Requirements`, they are your stopping condition.
> **When finishing**: follow the drafting rules of `human-ai-split` and `evidence-verification` if this repository has adopted them (see `docs/changes/README.md`). Never edit a proposal whose status is `implemented` or `superseded`.

**A controlled `touches` vocabulary**, declared in `docs/changes/README.md` once the repository holds more than about thirty proposals, so that search hits reliably.

**A validity rule**: `implemented` → constraint; `accepted` → constraint on design; `draft` → context only; `superseded`, `abandoned` → history.

## Rules

| ID | Rule | Principle |
|---|---|---|
| **AC1** | The repository MUST have an agent instruction file containing the block above (or its equivalent). | P3 |
| **AC2** | Before changing code, an agent MUST search proposals whose `touches` overlap and MUST treat the judgment sections of `implemented` proposals as constraints; if it must violate one, it MUST tell the person first. | P5 |
| **AC3** | An agent MUST treat `superseded` and `abandoned` proposals as history only. | P4 |
| **AC4** | `touches` SHOULD use a declared vocabulary once the repository holds more than about thirty proposals. | P7 |

## Cost

A few lines in the instruction file, one search per change, and keeping `touches` meaningful.

## Remove

Delete the block. Agents treat the repository as code only.
