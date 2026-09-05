# change-proposal

A practice for recording the *intent and judgment* behind a change to a product or system.

A **change proposal** records why a change is being made, what it deliberately leaves out, what was decided and rejected, and what risks were knowingly accepted. A person writes it, it lives in the repository, and it merges in the same pull request as the change. Six sections and an optional summary; that is the core. Everything else is a pattern.

> **Status: very early, and deliberately loose.** One real adoption so far. The practice is *described* here, not specified: no numbered rules, no requirement keywords, no fixed vocabulary, because too much is still uncertain to freeze. Patterns are how the practice is meant to grow: optional additions a team adopts when it meets the situation, combines as it needs, and drops without touching what was written. The eighteen pages under `docs/patterns/` are **candidates** for that system, not validated members of it: every one was written before anyone met its situation. As adoptions meet them, each is validated as a pattern, absorbed into the core, or dropped.

## Where to read

| Path | What |
|---|---|
| [`docs/guide.md`](docs/guide.md) | The practice, explained once: what a proposal is, when to write one, what goes in each section and why, what it is not |
| [`docs/patterns/README.md`](docs/patterns/README.md) | What a pattern is, and the candidate patterns organized by the question each answers |
| `docs/patterns/<name>.md` | One page per candidate: what it is for, when you would want it, what it adds, what it costs |
| [`templates/change-proposal.md`](templates/change-proposal.md) | The template |
| `docs/changes/` | This repository's own proposals |

This repository contains documents only. It ships no scripts, skills or configuration; the patterns that involve tooling (`lint-gate`, `agent-skills`, `agent-context`) say what the tooling should do and leave the implementation to adopters.

## The practice in five lines

1. A change that alters observable behavior gets a proposal at `docs/changes/YYYY-MM-DD-<slug>.md`, in the same PR as the code. No behavior change: the PR description says so.
2. The proposal has six sections, **Problem**, **Goals**, **Non-Goals**, **Requirements**, **Decisions**, **Risks**, plus an optional **Summary** up top.
3. It records what the code cannot: why, what was left out, what was rejected and why, what was knowingly accepted.
4. A person writes it, or explicitly approves every section. Empty sections are deleted.
5. Nothing else is required. When you meet a situation the core does not cover, adopt the pattern for it. The ones written so far are candidates, so say how it went.

## Patterns, not a process

The core does not define a lifecycle, metadata, sizing, review stages, how AI assistants participate, what happens to a merged proposal, which language it is written in, or any tooling. Each of those is left to a pattern: an optional, composable addition with a stated situation that calls for it, adopted when the situation appears and dropped without touching what was written. That is the intended way to extend the practice.

What is not settled is the catalog's contents. The patterns written so far are candidates: each may be validated by use, absorbed into the core, or dropped. See [`docs/patterns/README.md`](docs/patterns/README.md).

## Contributing

Changes to this repository use the practice on itself: a change to what the practice asks for gets a proposal in `docs/changes/`. See [`CONTRIBUTING.md`](CONTRIBUTING.md).
