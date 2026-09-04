# Pattern: decision-promotion

Separates decisions that belong to one change from decisions that constrain every future change, and gives the latter a home that is not buried in a proposal about something else.

**When.** The same decision is cited from three or more proposals, or a newcomer asks "where is it written that we do X?" and the answer is "in the proposal about Y".

**Goes with.** `agent-context` (accepted decision records are agent constraints), `supersession` (decision records follow the same immutability), `proposal-metadata` (records link back by id).

## What it adds

**A directory**: `docs/decisions/`, holding decision records named `NNNN-<slug>.md`.

**A record template**:

```
# ADR-NNNN: [the decision in one sentence]
Status: accepted            (proposed | accepted | superseded | deprecated)
Origin: docs/changes/YYYY-MM-DD-<slug>.md   (the proposal where it was first made)

## Context
(the situation that made the decision necessary, 2–4 sentences; evidence lives in the origin proposal)

## Decision
(one paragraph, imperative: "When doing X, use Y. Do not use Z.")

## Rejected alternatives
- (alternative): (reason). Revisit when:

## Consequences
- Enforces:
- Gives up:
- Exceptions: (who approves)
```

**A promotion step.** When a proposal's `Decisions` contains a decision that is really a standard, the author writes the record in the same pull request and replaces the decision text with `→ ADR-NNNN`. The record cites the proposal as its origin.

**A constraint for agents** (with `agent-context`): `accepted` records are repository-wide constraints.

## Using it

- The test for "standard or local?" is whether the decision would constrain a change in an unrelated area. If yes, promote it.
- The proposal points at the record and the record cites the proposal, so either can be found from the other.
- Records are not edited once `accepted`; they are superseded, like proposals.

## Cost

An occasional extra file, and the judgment "standard or local?".

## Removing it

Stop promoting. Existing records remain valid.
