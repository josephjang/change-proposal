# change-proposal

A practice for recording the *intent and judgment* behind a change to a product or system. The core is simple; the practice is built to be extended.

A **Change Proposal (CP)** records why a change is being made, what it deliberately leaves out, what was decided and rejected, and what risks were knowingly accepted. It is written by a person, lives in the repository, and is merged in the same pull request as the change. A proposal is not bound to one shape — it can be a set of documents, and it need not be markdown — but the core specifies one concrete form: a single one-page markdown file. Only that form is specified today.

That is the whole core. Everything else — sizing, review stages, AI-drafting rules, immutability, metadata, agent integration, tooling, translations — is a **pattern**: documented, optional, adoptable independently, and never assumed by the core.

> **Status: very early.** One real adoption so far, and it exercised the core. Deliberately not settled yet: whether **patterns** are the right extension mechanism — today's catalog is a set of candidates, written ahead of adoption; and whether starting from the core alone is right for every team, or some conditions justify starting larger.

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
2. The proposal has six sections — **Problem**, **Goals**, **Non-Goals**, **Requirements**, **Decisions**, **Risks** — plus an optional **Summary** up top.
3. It records what the code cannot: why, what was left out, what was rejected and why, what was knowingly accepted.
4. A person writes it. It fits on one page. Empty sections are deleted.
5. Nothing else is required. Add a pattern when its signal appears.

## Patterns, not a process

The core does not define a lifecycle, metadata, sizing, review stages, how AI assistants participate, what happens to a merged proposal, which language it is written in, or any tooling. Each of those is a pattern with a stated signal for adoption. See `docs/patterns/README.md`.

## Contributing

Changes to this repository use the practice on itself: a change to the concept, a rule, a pattern or the template gets a proposal in `docs/changes/`. See `CONTRIBUTING.md`.
