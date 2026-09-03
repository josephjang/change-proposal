# change-proposal

A minimal practice for recording the *judgment* behind a change to a product or system, with a catalog of patterns that can be added later — one at a time, when needed.

A **Change Proposal (CP)** is a one-page markdown file that says why a change is being made, what it deliberately leaves out, what was decided and rejected, and what risks were knowingly accepted. It is written by a person, lives in the repository, and is merged in the same pull request as the change.

That is the whole core. Everything else — sizing, review stages, AI-drafting rules, immutability, metadata, agent integration, tooling, translations — is a **pattern**: documented, optional, adoptable independently, and never assumed by the core.

## Documents

| Path | What |
|---|---|
| `docs/concept.md` | What a Change Proposal is, what it is not, what the core deliberately leaves undefined |
| `docs/principles.md` | Eleven principles and the reasoning behind them |
| `docs/rules.md` | The core rules — eight of them. Pattern rules live in the pattern cards |
| `docs/patterns/README.md` | The pattern catalog: what each adds, its signal, how patterns combine, example compositions |
| `docs/patterns/<name>.md` | One card per pattern, self-contained: intent, signal, what it adds, its rules, cost, removal |
| `templates/change-proposal.md` | The core template |
| `docs/changes/` | This repository's own proposals |

This repository contains documents only. It ships no scripts, skills, configuration files or templates beyond the core one; patterns that involve tooling (`lint-gate`, `agent-skills`, `agent-context`) describe what the tooling must do and leave the implementation to adopters.

## The core in five lines

1. A change that alters observable behavior gets a proposal at `docs/changes/YYYY-MM-DD-<slug>.md`, in the same PR as the code. No behavior change → the PR description says so.
2. The proposal has four sections — **Problem**, **Non-Goals**, **Decisions**, **Risks** — plus an optional **Summary** up top.
3. It records what the code cannot: why, what was left out, what was rejected and why, what was knowingly accepted.
4. A person writes it. It fits on one page. Empty sections are deleted.
5. Nothing else is required. Add a pattern when its signal appears.

## Patterns, not a process

The core does not define a lifecycle, metadata, sizing, review stages, how AI assistants participate, what happens to a merged proposal, which language it is written in, or any tooling. Each of those is a pattern with a stated signal for adoption. See `docs/patterns/README.md`.

## Language

The practice's documents are English only. Whether proposals themselves may be written in another language is the `multilingual-records` pattern.

## Contributing

Changes to this repository use the practice on itself: a change to the concept, a rule, a pattern or the template gets a proposal in `docs/changes/`. See `CONTRIBUTING.md`.
