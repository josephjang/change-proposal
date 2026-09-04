# Pattern: living-docs-bridge

Keeps the documents that describe *current state* honest by making every change that alters the state say which of them it updated.

**When.** Someone answers "how does this work today?" by reading several proposals in order, or a README is found describing a structure that stopped existing three proposals ago.

**Needs.** One of `risk-signals` or `sizing-tiers`, to define which proposals carry the section. Goes with `supersession` (immutable ledger plus maintained state is the intended pair), `agent-context` (the agent instruction file is a living document), `lint-gate`.

## What it adds

**One section**, expected in proposals with a risk signal (or tier T2 and above) and optional otherwise, placed last:

```
## Living docs
- `docs/architecture.md` — (what changed)
- `README.md` — (what changed)
- or: no update needed — (reason)
```

**A reviewer step.** Check the list against the document changes in the pull request. A listed document that did not change, or a changed document that is not listed, is a review comment.

**A minimum set of living documents** the repository keeps: a README, an architecture note, an agent instruction file if agents work there, runbooks where operations exist. Living documents may cite the proposal that caused a structural change.

## Using it

- A proposal with a risk signal (or tier T2 and above) includes `Living docs`, listing the updated current-state documents by path, or "no update needed" with the reason.
- The reviewer checks the list against what the pull request actually touched.
- The living documents have to exist for the section to mean anything.

## Cost

One or two lines per risky change and one reviewer glance. The real cost is maintaining the living documents themselves.

## Removing it

Drop the section. Living documents will drift; that is the trade.
