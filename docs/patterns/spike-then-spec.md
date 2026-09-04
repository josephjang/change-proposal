# Pattern: spike-then-spec

Makes "build to learn, then write the proposal" a first-class path, so that proposals are written from knowledge rather than to justify a prototype that already exists.

**When.** Proposals are being written after the fact to rationalize prototypes, or authors skip the proposal because "we did not know what we were building until we built it".

**Needs.** `proposal-metadata` for the `abandoned` status; without it, an abandoned note is a proposal whose title starts with "Abandoned:". Goes with `design-first-review` (defines when a prototype may merge) and `supersession` (abandoned notes are records too).

## What it adds

**One status value**: `abandoned`.

**An abandoned note**: a three-section proposal for a discarded spike. `Problem` (what was being explored), `Decisions` (what was tried and why it was dropped), `Risks` used as "what we learned". A few lines. Its value is that the next person does not spend the same afternoon.

## Using it

- Experimental work on a branch that never reaches the main branch needs no proposal. Explore freely.
- A proposal exists before experimental code reaches the main branch, even behind a flag. With `design-first-review`, that means before `accepted`.
- A discarded spike leaves an `abandoned` note recording what was tried and what was learned.

## Cost

None per change. One discipline: noticing the moment a spike turns into a change.

## Removing it

Without this pattern the guide reads as "the proposal comes first", and teams that prototype will quietly work around it.
