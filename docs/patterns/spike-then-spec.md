# Pattern: spike-then-spec

- **Requires**: core; `proposal-metadata` for the `abandoned` status (without it, an abandoned note is a proposal whose title starts with "Abandoned:")
- **Combines with**: `design-first-review` (defines when a prototype may merge), `supersession` (abandoned notes are records too)
- **Conflicts with**: —

## Intent

Make "build to learn, then write the proposal" a first-class path, so that proposals are written from knowledge rather than to justify a prototype that already exists.

## Signal

Proposals are being written after the fact to rationalize prototypes, or authors skip the proposal because "we did not know what we were building until we built it".

## Adds

**Three rules** and **one status value** (`abandoned`).

**An abandoned note** — a three-section proposal for a discarded spike: `Problem` (what was being explored), `Decisions` (what was tried and why it was dropped), `Risks` used as "what we learned". A few lines. Its value is that the next person does not spend the same afternoon.

## Rules

| ID | Rule | Principle |
|---|---|---|
| **SP1** | Experimental work on a branch that never reaches the main branch needs no proposal. | P10 |
| **SP2** | A proposal MUST exist before experimental code reaches the main branch, even behind a flag. With `design-first-review`, DF2 applies. | P3 |
| **SP3** | A discarded spike SHOULD leave an `abandoned` note recording what was tried and what was learned. | P4 |

## Cost

None per change. One discipline: noticing the moment a spike turns into a change.

## Remove

Drop SP1–SP3. Without this pattern the core reads as "the proposal comes first", and teams that prototype will quietly violate it.
