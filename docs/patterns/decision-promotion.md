# Pattern: decision-promotion

- **Requires**: core
- **Combines with**: `agent-context` (accepted decision records are agent constraints), `supersession` (decision records follow the same immutability), `proposal-metadata` (records link back by id)
- **Conflicts with**: —

## Intent

Separate decisions that belong to one change from decisions that constrain every future change, and give the latter a home that is not buried in a proposal about something else.

## Signal

The same decision is cited from three or more proposals, or a newcomer asks "where is it written that we do X?" and the answer is "in the proposal about Y".

## Adds

**A directory**: `docs/decisions/`, holding decision records named `NNNN-<slug>.md`.

**A record template**:

```
# ADR-NNNN: [the decision in one sentence]
Status: accepted            (proposed | accepted | superseded | deprecated)
Origin: docs/changes/YYYY-MM-DD-<slug>.md   (the proposal where it was first made)

## Context
(the situation that made the decision necessary — 2–4 sentences; evidence lives in the origin proposal)

## Decision
(one paragraph, imperative: "When doing X, use Y. Do not use Z.")

## Rejected alternatives
- (alternative): (reason). Revisit when:

## Consequences
- Enforces:
- Gives up:
- Exceptions: (who approves)
```

**A promotion step**: when a proposal's `Decisions` contains a decision that is really a standard, the author writes the record in the same pull request and replaces the decision text with `→ ADR-NNNN`. The record cites the proposal as its origin.

**A constraint for agents** (with `agent-context`): `accepted` records are repository-wide constraints.

## Rules

| ID | Rule | Principle |
|---|---|---|
| **DP1** | A decision that constrains future changes beyond the one that made it SHOULD be promoted to a decision record. | P2, P8 |
| **DP2** | The proposal's `Decisions` MUST reference the record it was promoted to, and the record MUST cite the originating proposal. | P7 |
| **DP3** | Decision records MUST NOT be edited once `accepted`; they are superseded like proposals. | P4 |

## Cost

An occasional extra file, and the judgment "standard or local?" — the test is whether it would constrain a change in an unrelated area.

## Remove

Stop promoting. Existing records remain valid.
