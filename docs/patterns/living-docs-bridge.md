# Pattern: living-docs-bridge

- **Requires**: core; one of `risk-signals` or `sizing-tiers` (to define which proposals must carry the section)
- **Combines with**: `supersession` (immutable ledger + maintained state is the intended pair), `agent-context` (the agent instruction file is a living document), `lint-gate`
- **Conflicts with**: —

## Intent

Keep the documents that describe *current state* honest by making every change that alters the state say which of them it updated.

## Signal

Someone answers "how does this work today?" by reading several proposals in order, or a README is found describing a structure that stopped existing three proposals ago.

## Adds

**One section**, required for proposals with a risk signal (or tier ≥ T2) and optional otherwise, placed last:

```
## Living docs
- `docs/architecture.md` — (what changed)
- `README.md` — (what changed)
- or: no update needed — (reason)
```

**A reviewer step**: check the list against the document changes in the pull request. A listed document that did not change, or a changed document that is not listed, is a review comment.

**A minimum set of living documents** the repository keeps: a README, an architecture note, an agent instruction file if agents work there, runbooks where operations exist. Living documents may cite the proposal that caused a structural change.

## Rules

| ID | Rule | Principle |
|---|---|---|
| **LD1** | A proposal with a risk signal (or tier ≥ T2) MUST include `Living docs`, listing updated current-state documents by path or "no update needed" with the reason. | P8 |
| **LD2** | The reviewer MUST check the list against the document changes in the pull request. | P8 |
| **LD3** | The repository SHOULD keep at least a README, an architecture note, and — where applicable — an agent instruction file and runbooks. | P8 |

## Cost

One or two lines per risky change and one reviewer glance. The real cost is that the living documents must exist.

## Remove

Drop the section. Living documents will drift; that is the trade.
