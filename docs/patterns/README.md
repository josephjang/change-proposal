# Patterns

The [guide](../guide.md) describes the core: a proposal for every change that alters observable behavior, written by a person, living beside the code, with six sections and an optional summary. A team can use the core alone. A **pattern** is how the practice grows beyond it. It is an optional addition (a section, a field, a step, a document, a tooling requirement) that a team adopts when it meets the situation the pattern names, combines with other patterns as it needs, and drops again without touching what was already written. The core never assumes one; a team that has not adopted a pattern is not missing it, it has not met the situation yet.

> **Status: candidates.** Nothing below has been validated, and most of these pages were written before anyone met the situation they name: they are thought-through answers, kept as a shelf to reach for when you meet one of these situations, not as a menu to work through. Every entry can still be validated, absorbed into the core, or dropped, as [Adding, validating, absorbing, retiring](#adding-validating-absorbing-retiring) describes. Expect entries to move, change or leave.

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

## Saying which patterns you use

A repository says which patterns it uses in a sentence at the top of its `docs/changes/README.md`, so that a reader of the proposals knows what to expect. Where a pattern has a knob (a word cap, a reviewer count, a turnaround), its page names it and gives a default, and this sentence is where a team writes the value it chose:

> This repository uses change proposals with `risk-signals`, `verification`, `human-ai-split` and `evidence-verification`. Reviewers on a risk signal: 1. Record language: English.

That sentence is the whole mechanism. Patterns that bring tooling (`lint-gate`, `agent-skills`) may turn it into a configuration file; the sentence remains the version people read. Dropping a pattern is deleting it from the sentence; proposals already written under it stay as they are, and each page says what else changes.

Before settling on a set, read [How they fit together](#how-they-fit-together): several patterns need another one adopted alongside them, and a set that leaves a needed pattern out does not work.

## How they fit together

Each pattern adds something to a proposal or to the process around it. None changes what the guide describes, and none rewrites another's addition, so that several can be adopted at once. Section names come from one shared list (below), so that a proposal written under several still reads as one document and a reader finds the same name in every proposal.

A few lean on another. `supersession`, `sizing-tiers`, `design-first-review`, `initiative-umbrella` and `agent-context` need the front matter that `proposal-metadata` adds; `evidence-verification` tightens the section that `verification` adds; `design-first-review` and `living-docs-bridge` need `risk-signals` or `sizing-tiers` to know which proposals they apply to; `agent-context` needs `supersession`, because it assumes merged proposals are not edited in place and an agent cannot otherwise tell which proposals still hold. Each page says what it needs.

## Sections a proposal may carry

The guide's sections and every section a pattern adds, in one place. A proposal starts from the [template](../../templates/change-proposal.md) and grows by adding rows from this list; no pattern renames one.

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
| `Outcome`, `What we learned`, `Follow-ups`, `Process retrospective` | `outcome-review` | outcome review documents only |

Headings in another language are the `multilingual-records` pattern.

## Starting points

Combinations that have been thought through together, for a team adopting several at once. Not prescriptions, and, like the patterns themselves, not yet validated.

| Situation | Patterns | Notes |
|---|---|---|
| One person or a very small team, assistants used daily | `risk-signals`, `verification`, `human-ai-split`, `evidence-verification` | The smallest combination that keeps AI drafting honest. |
| A product team with a few shared contracts | + `proposal-metadata`, `supersession`, `agent-context`, `living-docs-bridge`, `spike-then-spec` | Merged proposals become agent constraints; state documents stay honest. |
| A platform team whose output is contracts | + `sizing-tiers`, `design-first-review`, `decision-promotion`, `lint-gate` | Pre-code review is enforceable; standards have a home. |
| Several teams running quarterly initiatives | + `initiative-umbrella`, `outcome-review` | Work larger than one proposal, with its outcome revisited. |
| Any of the above, in Korean | + `multilingual-records` | Headings carry the English name; everything machine-facing stays English. |

Changing the set is editing the sentence in `docs/changes/README.md` ([Saying which patterns you use](#saying-which-patterns-you-use)); nothing already written changes.

## Adding, validating, absorbing, retiring

A new pattern arrives as a change to this repository ([CONTRIBUTING](../../CONTRIBUTING.md)). It should say what situation it answers, ideally one somebody actually met, what it adds, and what every change pays while it is on. A pattern that cannot name its situation is ceremony looking for a home.

Validating a candidate, absorbing it into the core, or retiring it arrives the same way, and the evidence is adoptions: what a team learns from a pattern, whether it wished every proposal had carried it or whether it was ceremony, is what settles it. If you have adopted one, say so on its page. An adoption report is a pull request, no proposal of its own: your account of what the candidate did, in your own words and under your name, as an entry under an `## Adoption reports` heading at the end of the page. It is not asked for a verdict; the proposal that settles the candidate is written later, by the maintainer, from the reports the page has collected ([CONTRIBUTING](../../CONTRIBUTING.md)).

A candidate every adopter picks up early is core material. That has happened once, before this catalog was published: `success-criteria` began as a pattern, and the two sections it added, `Goals` and `Requirements`, became core sections when the first adoption needed both from day one ([D6](../changes/2026-08-30-initial-release.md)). A candidate that holds up where its situation appears is a validated pattern. One nobody meets, or one whose answer does not hold up when they do, is retired: dropped from the catalog.
