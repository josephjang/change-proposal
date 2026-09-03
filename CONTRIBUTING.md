# Contributing

This repository uses the practice on itself. Its composition is stated at the top of `docs/changes/README.md`; its proposals live in `docs/changes/`.

## What needs a proposal

| Change | Proposal? |
|---|---|
| The concept, a principle, or a core rule changed in substance | Yes — every adopter depends on it (risk signal: contract) |
| A pattern added or removed, or its signal / requires / conflicts / rules changed | Yes — contract |
| A label added to the table in `docs/patterns/README.md` | Yes — contract |
| The core template changed in what it asks for | Yes — contract |
| Wording, examples, typos | No — PR description only |

## Procedure

1. Read the existing proposals in `docs/changes/` — the reasoning behind the current rule or pattern is there.
2. Write the proposal from `templates/change-proposal.md`. Its `Problem` must name the situation the current practice mishandled; a proposal that starts from a solution is sent back.
3. For a new pattern: show the signal, the per-change cost, and that it uses labels from the table — or why the table must grow.
4. Because these are contract changes, a reviewer reads the draft before the wording is finalized (`risk-signals`).

## Reviewing

Beyond the core rules and the adopted patterns' rules, the reviewer asks one question of every substantive change: *which principle does this serve, and which does it cost?* A change that cannot answer is declined.
