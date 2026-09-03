# Patterns

The core (`../concept.md`, `../rules.md`) is complete and small. Everything a team might want beyond it is a **pattern**: an optional addition that can be adopted, parameterized and removed on its own. This catalog lists them, says how they combine, and gives example compositions.

## What a pattern is

Every pattern card has the same parts:

- **Intent** — the one problem it solves.
- **Signal** — the observable situation that says it is time to adopt it. A pattern without a signal is ceremony (P10); none is listed here.
- **Adds** — sections (with their label), front-matter fields, steps, documents, or tooling requirements. Section text is given in the card, so the card is all a team needs.
- **Rules** — the pattern's own rules, with ids, in the same MUST/SHOULD/MAY form as the core.
- **Requires / Combines with / Conflicts with**.
- **Cost** — what every change pays while the pattern is on.
- **Remove** — how, and what happens to proposals written under it (almost always: nothing; they remain valid).

## Catalog

| Pattern | Intent | Signal | Adds |
|---|---|---|---|
| [`risk-signals`](risk-signals.md) | Pre-code review and a rollout block for contract, irreversible and sensitive-area changes | The first change someone wishes had been discussed before it was built | Three questions; `Rollout & rollback`, `Cross-cutting concerns`; a reviewer before code |
| [`proposal-metadata`](proposal-metadata.md) | Front matter: owner, status, links, tags | Proposals need to be found by something other than date, or a change spans several PRs | Front matter block and fields; `status` |
| [`supersession`](supersession.md) | Merged proposals are immutable and reversed by new ones | Someone wants to "fix" a merged proposal | `supersedes` / `superseded_by`; a reversal procedure |
| [`human-ai-split`](human-ai-split.md) | Assistants draft what is derivable; people write judgment; drafts are marked | An assistant is used to write any part of a proposal | Section classification; `<!-- ai-draft -->` marker; an instruction to assistants |
| [`evidence-verification`](evidence-verification.md) | Verification is commands and observations only | An assistant implements or tests | The strict section shape; a reviewer test; an agent rule |
| [`success-criteria`](success-criteria.md) | A true/false definition of done | "Is it done?" is disputed, or someone else implements from the proposal | `Goals`, `Requirements` |
| [`before-after`](before-after.md) | Describe what changed for readers who will not open the diff | Proposals are read months later or by agents, and the change cannot be reconstructed | `Change` (before / after / where) |
| [`sizing-tiers`](sizing-tiers.md) | Explicit T0–T3 tiers with a rubric | Recurring after-the-fact arguments about how much review a change deserved | `tier` field; rubric; per-tier caps |
| [`design-first-review`](design-first-review.md) | A docs-only PR reaches `accepted` before implementation | Risky changes arrive as finished code and reviewers cannot push back | `accepted` status; `Open questions`; two-stage flow |
| [`spike-then-spec`](spike-then-spec.md) | Build to learn, then write the proposal | Proposals are written to justify prototypes that already exist | Three rules; `abandoned` status |
| [`living-docs-bridge`](living-docs-bridge.md) | Each risky change names the current-state documents it updated | "How does this work today?" needs several proposals | `Living docs` |
| [`decision-promotion`](decision-promotion.md) | Decisions that outlive a change move to decision records | The same decision is cited from three or more proposals | `docs/decisions/`; a record template |
| [`initiative-umbrella`](initiative-umbrella.md) | Brief + design + child proposals for multi-week work | A month-plus, multi-team initiative starts | Initiative directory; brief and design documents; `parent` |
| [`outcome-review`](outcome-review.md) | Compare declared metrics with actuals after launch | Metrics are declared and never revisited | `outcome.md`; a schedule |
| [`agent-context`](agent-context.md) | Coding agents read merged proposals as constraints | An agent rebuilds a rejected alternative or does a non-goal | An agent instruction block; `touches` vocabulary |
| [`agent-skills`](agent-skills.md) | Skills for Claude Code and Codex that do the mechanical parts | The same instructions are pasted into every session | Skill specifications (what each must do) |
| [`lint-gate`](lint-gate.md) | CI enforces the mechanical rules | A proposal merged with markers, or a behavior change merged without one | A lint specification; enforcement levels |
| [`multilingual-records`](multilingual-records.md) | Proposals in a non-English language stay machine-readable | The team writes in more than one language | A heading rule; invariants |

## Section labels

One table for the core and every pattern. No pattern renames a section; a proposal grows by adding rows from this table.

| Label | Introduced by | Replaces |
|---|---|---|
| `Problem` | core | |
| `Non-Goals` | core | |
| `Decisions` | core | |
| `Product Decisions`, `Technical Decisions` | core | `Decisions` (together, when both kinds are present) |
| `Verification` | core | |
| `Risks & deferred` | core | |
| `Goals` | `success-criteria` | |
| `Requirements` | `success-criteria` | |
| `Change` | `before-after` | |
| `Summary` | `sizing-tiers` (T2+), `initiative-umbrella` | |
| `Rollout & rollback` | `risk-signals` | |
| `Cross-cutting concerns` | `risk-signals` | |
| `Open questions` | `design-first-review` | |
| `Living docs` | `living-docs-bridge` | |
| `Current structure`, `Design`, `Milestones` | `initiative-umbrella` (brief and design documents only) | |
| `Outcome` | `outcome-review` | |

Non-English labels are the `multilingual-records` pattern.

## Composition

1. **The core is always on.** Every pattern requires it.
2. **Patterns are additive.** Each adds sections, fields, steps or rules; none rewrites another's. The shared label table (P7) is what makes this hold.
3. **Requirements are declared on the card.** Most patterns need only the core. Some need another pattern (for example `supersession` needs `proposal-metadata` for its `status` field, and `design-first-review` needs `risk-signals` or `sizing-tiers` to know which proposals get the stage).
4. **Conflicts are declared, not discovered.** There is one: editing merged proposals in place (no `supersession`) is incompatible with `agent-context`, because agents cannot tell which proposals are current.
5. **A repository's rules are the core rules plus the rules of its adopted patterns.** Nothing else binds.
6. **Removal is legitimate.** Each card says how. Proposals written under a removed pattern stay as they are.
7. **Parameters belong to the adopter.** Where a pattern has a knob (a word cap, a reviewer count, a review SLA), the card names it and gives a default; the value is recorded in the repository's `docs/changes/README.md`.

## Declaring a composition

A repository states its composition in prose at the top of `docs/changes/README.md`:

> This repository uses the change-proposal core with `risk-signals`, `human-ai-split` and `evidence-verification`. Reviewers on a risk signal: 1. Word cap: one page.

That is the whole mechanism. Patterns that bring tooling (`lint-gate`, `agent-skills`) may formalize the same statement into a configuration file; the prose remains the source of truth for people.

## Example compositions

Starting points, not prescriptions. Each is the core plus the listed patterns.

| Situation | Patterns | Notes |
|---|---|---|
| One person or a very small team, assistants used daily | `risk-signals`, `human-ai-split`, `evidence-verification` | The smallest composition that keeps AI drafting honest. |
| A product team with a few shared contracts | + `proposal-metadata`, `supersession`, `agent-context`, `living-docs-bridge`, `spike-then-spec` | Merged proposals become agent constraints; state documents stay honest. |
| A platform team whose output is contracts | + `sizing-tiers`, `design-first-review`, `decision-promotion`, `lint-gate` | Pre-code review is enforceable; standards have a home. |
| Several teams running quarterly initiatives | + `initiative-umbrella`, `outcome-review`, `success-criteria` | Work larger than one proposal, with its outcome revisited. |
| Any of the above, in Korean | + `multilingual-records` | Headings carry the English label; everything machine-facing stays English. |

Moving between compositions is adding or removing lines in `docs/changes/README.md`. Nothing already written changes.

## Proposing a new pattern

A new pattern is a change to this repository and arrives as a proposal (`../../CONTRIBUTING.md`). It must show the signal — a real situation the existing patterns did not handle — and its per-change cost, and it must use labels from the table above or explain why the table must grow. A pattern that cannot name a signal is declined.
