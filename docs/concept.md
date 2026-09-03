# Concept: the Change Proposal

## Definition

A **Change Proposal** (CP) is a one-page markdown file that records the judgment behind one change to a product or system: why it is being made, what it deliberately leaves out, what was decided and what was rejected, and what risks were knowingly accepted. A person writes it, it lives in the repository, and it is merged in the same pull request as the change.

Three properties define it.

- **It records judgment, not description.** Code, schemas and interfaces describe themselves. A proposal holds what code cannot recover.
- **It travels with the change.** Same repository, same pull request, same review, same history. After the merge it is the change's record.
- **It is small.** One page. Four sections and an optional summary. Anything that would make it larger is either description (and belongs in the code) or a pattern (and belongs in the catalog).

## Why "proposal"

The word is chosen because the document's first job is to put an intent in front of a reviewer alongside the work, and because — unlike a spec — it does not try to describe the solution. It proposes: here is the problem, here is what we will not do, here is what we decided and gave up. After the merge it is still called a proposal; its position on the main branch says it was carried out.

## The core

**Trigger.** A change that alters observable behavior gets a proposal. A change that does not — a refactor with identical behavior, a typo, a dependency patch, tests only — does not; its pull-request description says so and says how that was checked.

**Location.** `docs/changes/YYYY-MM-DD-<slug>.md`, committed in the same pull request as the code.

**Title.** `Change Proposal: <change name>`. The path and file name already say what the document is, but a reader of the document alone may never look at them. A repository that already identifies documents its own way — an id scheme in the tradition of KIP-123, a date — may use that marker in place of the prefix.

**Shape.** A title, an optional summary, and four sections with fixed labels:

| Section | Holds |
|---|---|
| **Summary** (optional) | Three to five sentences directly under the title: what changes, why, what does not change. |
| **Problem** | What is wrong now, for whom, with the evidence. How it works today and why it was built that way, when that matters. Not "what we will build". |
| **Non-Goals** | What this change deliberately does not do, and why — decided at scoping or discovered during the work. At least one. The line that stops the change from growing. |
| **Decisions** | Only decisions that had alternatives. For each: what was chosen, what was rejected, and a reason of the kind that would change if the facts changed. Deleted if there were none. May be split into **Product Decisions** and **Technical Decisions** when both kinds are present: reversing a product decision changes what the team experiences or what a standard means; reversing a technical one changes only the code. |
| **Risks** | Trade-offs accepted knowingly, with the reason. |

**Authorship.** A person writes it. Whether and how an assistant helps is not defined by the core.

**Size.** One page. A section with nothing to say is deleted, not filled.

**Nothing else.** No front matter, no status field, no tier, no review stage, no marker, no configuration.

## What the core deliberately leaves undefined

The core is complete as a practice: a team can use it alone for years. It is also silent, on purpose, about everything that a team might need later. Each silence is filled by a pattern — and only when the team meets the situation the pattern names.

| The core does not say… | …because that is the pattern |
|---|---|
| how big a change must be before it needs more than one page, or more than one reviewer | `risk-signals`, `sizing-tiers` |
| what happens to a proposal after it is merged — whether it may be edited, how it is reversed | `supersession` |
| what a proposal's metadata is — owner, status, links, tags | `proposal-metadata` |
| what "done" means | `success-criteria` |
| whether the proposal records what was verified | `verification` |
| how to describe what changed, for readers who will not open the diff | `before-after` |
| whether a proposal is reviewed before the code is written | `design-first-review` |
| what to do with prototypes and experiments | `spike-then-spec` |
| how AI assistants may participate in writing it | `human-ai-split` |
| what counts as evidence in `Verification` | `evidence-verification` |
| how current-state documents stay honest | `living-docs-bridge` |
| where decisions that outlive a change go | `decision-promotion` |
| how work larger than one proposal is organized | `initiative-umbrella` |
| whether anyone looks at the outcome later | `outcome-review` |
| how coding agents use proposals | `agent-context`, `agent-skills` |
| whether anything is enforced by tooling | `lint-gate` |
| which language proposals are written in | `multilingual-records` |

A team that has not adopted a pattern is not "missing" it. It has not met the signal.

## What it is not

| Not a… | Because… |
|---|---|
| Product requirements document | A PRD describes a product area; a proposal describes one change, and only what code cannot say. |
| Design document or RFC | A design document describes a solution; a proposal describes the decisions inside it and points at the code for the rest. |
| Architecture decision record | An ADR holds a decision that outlives any single change; a proposal holds the decisions within one change. (`decision-promotion` connects them.) |
| Pull-request description | A PR description explains a diff to its reviewer and is forgotten. A proposal is written to be found later. For changes with no behavior change, the PR description is the whole record. |
| Changelog entry | A changelog says what changed for users; a proposal says why, what was rejected, what was accepted. |
| Ticket | A ticket tracks work; a proposal holds reasoning. They link to each other. |
| Wiki page | A wiki page describes current state and is edited in place; a proposal describes one transition. |
| Session transcript | A transcript with an assistant is raw material; a proposal is what a person distilled from it. |

## Sizing: blast radius, not diff size

The core has exactly one sizing question — *does behavior change?* — and it is answered by looking at what the change does, never at how many lines it touches, how long it took, or whether a person or an assistant wrote the code. A 2,000-line mechanical refactor with identical behavior needs no proposal. A one-line change to a permission check needs one. Finer sizing is the `risk-signals` and `sizing-tiers` patterns.

## The setting

The practice is shaped for teams that build with AI assistance, where code, summaries and verification logs are cheap to produce. That is why the core is small (drafting is free, so length is the failure mode), why it insists on judgment over description (description is what assistants do best and what goes stale first), and why the `verification` pattern asks what was *observed* rather than what was done. But the core itself makes no assumption about assistants. How they participate is the `human-ai-split` pattern; how they read proposals is `agent-context`.

## Vocabulary

| Term | Meaning |
|---|---|
| **Change** | One intentional modification to a product or system, delivered through a pull request. |
| **Proposal** | The document defined above. Abbreviated CP. Also the record of the change after the merge. |
| **Section** | One of the four core parts, the optional summary, or a part added by a pattern. |
| **Label** | The fixed English name of a section (`Problem`, `Decisions`, …). Patterns add labels from one shared table (`docs/patterns/README.md`). |
| **Judgment** | Content that only a person can supply: framing, boundaries, decisions and their reasons, what is accepted. The four core sections are judgment; `Verification`, where adopted, is judgment about evidence. |
| **Pattern** | An optional, independently adoptable addition to the core, with a stated signal. Documented in `docs/patterns/`. |
| **Signal** | The observable situation that says it is time to adopt a pattern. |
| **Composition** | The set of patterns a repository has adopted, stated in its `docs/changes/README.md`. |
