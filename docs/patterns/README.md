# Patterns

The [guide](../guide.md) describes a complete practice. Everything here is optional: something a team may add when it meets the situation the pattern names. None is assumed by the guide, none is required, and each can be dropped again.

> **Status: candidates.** Every pattern here was written before anyone met its situation in the field. They are kept as a shelf of thought-through answers, not as a menu to work through, and whether "patterns" is the right way to extend the practice at all is one of the open questions named in the [README](../../README.md). Expect entries to change or leave.

## By the question they answer

| When you find yourself asking… | Look at | It adds |
|---|---|---|
| Should this change have been discussed before it was built? | [`risk-signals`](risk-signals.md) | Three questions; `Rollout & rollback` and `Cross-cutting concerns`; a reviewer before code |
| How much review does a change deserve? We keep arguing after the fact. | [`sizing-tiers`](sizing-tiers.md) | T0–T3 tiers with a rubric |
| Can a reviewer push back on a design before the code exists? | [`design-first-review`](design-first-review.md) | An `accepted` stage reached through a docs-only PR; `Open questions` |
| We built a prototype first. When does it need a proposal? | [`spike-then-spec`](spike-then-spec.md) | Build-to-learn as a first-class path; `abandoned` notes |
| Was this actually tested? Nobody can find the answer. | [`verification`](verification.md) | `Verification`: what was checked, and what was not |
| An assistant says it verified something. Did it? | [`evidence-verification`](evidence-verification.md) | Verification as commands and observations only |
| Who actually decided this? An assistant drafted it. | [`human-ai-split`](human-ai-split.md) | Draft markers; approval by a person, section by section |
| What did this change do? I do not want to open the diff. | [`before-after`](before-after.md) | `Change`: before, after, where |
| How do I find proposals by owner, area or status? | [`proposal-metadata`](proposal-metadata.md) | Front matter: owner, status, links, tags |
| Someone wants to "fix" a merged proposal. | [`supersession`](supersession.md) | Merged proposals stay as written and are reversed by new ones |
| How does this work today? I had to read five proposals. | [`living-docs-bridge`](living-docs-bridge.md) | `Living docs`: which current-state documents this change updated |
| Where is it written that we always do X? | [`decision-promotion`](decision-promotion.md) | Decision records for decisions that outlive a change |
| This is a quarter of work across teams, not one change. | [`initiative-umbrella`](initiative-umbrella.md) | A brief, a design, and ordinary proposals under them |
| We declared a metric. Did it move? | [`outcome-review`](outcome-review.md) | An outcome review after launch |
| An agent just rebuilt something a proposal rejected. | [`agent-context`](agent-context.md) | Merged proposals as constraints agents read first |
| We paste the same instructions into every agent session. | [`agent-skills`](agent-skills.md) | What a set of skills should do |
| A proposal merged with draft markers still in it. | [`lint-gate`](lint-gate.md) | Mechanical checks in CI |
| We write in Korean. Will tooling still find the sections? | [`multilingual-records`](multilingual-records.md) | A heading convention that keeps section names machine-readable |

## How they fit together

Each pattern adds something to a proposal or to the process around it: a section, a front-matter field, a step, a document, a tooling requirement. None changes what the guide describes, and none rewrites another's addition. Section names come from one shared list (below) so that a proposal written under several patterns still reads as one document.

A few patterns lean on another. `supersession`, `sizing-tiers`, `design-first-review`, `initiative-umbrella` and `agent-context` need the front matter that `proposal-metadata` adds; `evidence-verification` tightens the section that `verification` adds; `design-first-review` and `living-docs-bridge` need `risk-signals` or `sizing-tiers` to know which proposals they apply to. Each page says what it needs. One real incompatibility exists: `agent-context` assumes merged proposals are not edited in place (which is what `supersession` provides), because an agent cannot otherwise tell which proposals still hold.

Where a pattern has a knob (a word cap, a reviewer count, a turnaround), its page names it and gives a default.

A repository says which patterns it uses in a sentence at the top of its `docs/changes/README.md`:

> This repository uses change proposals with `risk-signals`, `verification`, `human-ai-split` and `evidence-verification`. Reviewers on a risk signal: 1. Record language: English.

That sentence is the whole mechanism. Patterns that bring tooling (`lint-gate`, `agent-skills`) may turn it into a configuration file; the sentence remains the version people read. Dropping a pattern is deleting it from the sentence; proposals already written under it stay as they are.

## Sections a proposal may carry

The guide's sections and every section a pattern adds, in one place. A proposal grows by adding rows from this list; no pattern renames one.

| Section | From | Notes |
|---|---|---|
| `Summary` | guide (optional) | |
| `Problem`, `Goals`, `Non-Goals`, `Requirements`, `Decisions`, `Risks` | guide | `Decisions` may be split into `Product Decisions` and `Technical Decisions` |
| `Change` | `before-after` | |
| `Verification` | `verification` | |
| `Rollout & rollback`, `Cross-cutting concerns` | `risk-signals` | |
| `Open questions` | `design-first-review` | |
| `Living docs` | `living-docs-bridge` | |
| `Current structure`, `Design`, `Milestones` | `initiative-umbrella` | brief and design documents only |
| `Outcome` | `outcome-review` | |

Headings in another language are the `multilingual-records` pattern.

## Starting points

Not prescriptions; combinations that hang together.

| Situation | Patterns | Notes |
|---|---|---|
| One person or a very small team, assistants used daily | `risk-signals`, `verification`, `human-ai-split`, `evidence-verification` | The smallest combination that keeps AI drafting honest. |
| A product team with a few shared contracts | + `proposal-metadata`, `supersession`, `agent-context`, `living-docs-bridge`, `spike-then-spec` | Merged proposals become agent constraints; state documents stay honest. |
| A platform team whose output is contracts | + `sizing-tiers`, `design-first-review`, `decision-promotion`, `lint-gate` | Pre-code review is enforceable; standards have a home. |
| Several teams running quarterly initiatives | + `initiative-umbrella`, `outcome-review` | Work larger than one proposal, with its outcome revisited. |
| Any of the above, in Korean | + `multilingual-records` | Headings carry the English name; everything machine-facing stays English. |

Moving between combinations is editing the sentence in `docs/changes/README.md`. Nothing already written changes.

## Adding one

A new pattern arrives as a change to this repository ([CONTRIBUTING](../../CONTRIBUTING.md)). It should say what situation it answers, ideally one somebody actually met, what it adds, and what every change pays while it is on. A pattern that cannot name its situation is ceremony looking for a home.
