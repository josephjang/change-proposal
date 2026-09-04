# Change Proposals

This is the whole practice, explained once. It is written to be understood rather than enforced: nothing here is numbered, nothing is a requirement keyword, and where the practice is unsure it says so.

## What a change proposal is

A **change proposal** records the intent and judgment behind one change to a product or system: why it is being made, what it deliberately leaves out, what was decided and what was rejected, and what risks were knowingly accepted. A person writes it, it lives in the repository, and it merges in the same pull request as the change.

Three things make it what it is.

- **It holds judgment, not description.** Code, schemas and interfaces describe themselves, and copied description goes stale the day after the merge. A proposal holds what the code cannot recover: the reasons.
- **It travels with the change.** Same repository, same pull request, same review, same history. A document that must be found somewhere else is not read, by people or by agents. After the merge it is the change's record.
- **It is small.** Six sections and an optional summary. Anything that would make it larger is either description, which belongs in the code, or something a team adds later when it needs it (see [Going further](#going-further)).

### Why "proposal"

The document's first job is to put an intent in front of a reviewer alongside the work, and, unlike a spec, it does not try to describe the solution. It proposes: here is the problem, here is what we will not do, here is what we decided and gave up. After the merge it is still called a proposal; its position on the main branch says it was carried out.

## When to write one

Write a proposal when a change alters observable behavior. Skip it when it does not: a refactor with identical behavior, a typo, a dependency patch, tests only. In that case the pull-request description says there is no behavior change and how that was checked.

That is the only sizing question, and it is answered by looking at what the change *does*, never at how many lines it touches, how long it took, or whether a person or an assistant wrote the code. A 2,000-line mechanical refactor with identical behavior needs no proposal. A one-line change to a permission check needs one. Diff size correlates badly with risk, and the correlation collapses entirely once assistants produce thousands of correct mechanical lines in minutes.

Finer sizing, such as which changes deserve a reviewer before the code is written, is a later addition ([`risk-signals`](patterns/risk-signals.md), [`sizing-tiers`](patterns/sizing-tiers.md)), not part of the basic practice.

## Where it lives

`docs/changes/YYYY-MM-DD-<slug>.md`, committed in the same pull request as the code. A proposal that is really a set of documents takes a directory at the same address, `docs/changes/YYYY-MM-DD-<slug>/`, and it need not be markdown. A repository with its own document location or naming convention uses that instead; what matters is that the proposal is found next to the code, not the exact path.

The title is `Change Proposal: <change name>`. The path already says what the document is, but a reader of the document alone may never look at the path. A repository that already marks its documents its own way, with an id scheme in the tradition of KIP-123 or a date, can use that marker instead.

## What goes in it

A title, an optional summary, and six sections with fixed names, in this order:

| Section | Holds |
|---|---|
| **Summary** (optional) | Three to five sentences directly under the title: what changes, why, what does not change. |
| **Problem** | What is wrong now, for whom, with the evidence. |
| **Goals** | The end states the change makes possible. |
| **Non-Goals** | What the change deliberately does not do, and why. |
| **Requirements** | Statements that can be judged true or false; when all are true, the work is done. |
| **Decisions** | Decisions that had alternatives: what was chosen, what was rejected, why. |
| **Risks** | Trade-offs accepted knowingly, with the reason. |

The names are fixed and in English so that a proposal from one repository reads like a proposal from another, and so that tooling and agents can find sections without guessing.

A section with nothing to say is deleted rather than filled: an empty heading tells the reader nothing, and a section filled for form teaches them to skip it next time. In practice that means `Decisions`, `Risks` and the optional `Summary`. A change worth a proposal always has a problem, a goal, something it will not do, and a way to tell when it is done.

Each section, in more detail:

### Summary

Optional. Three to five sentences directly under the title: what changes, why, what does not change. Useful when the proposal is long enough that a reader wants the shape before the detail. Delete it when the proposal is short enough to speak for itself.

### Problem

What is wrong right now, for whom, and the evidence: an issue, a metric, a request. Where it matters, how it works today and why it was built that way; the diff shows only "after", and the reason for the old shape is exactly what the next person will not be able to recover.

`Problem` is not "what we will build". A proposal that starts from a solution has skipped the part a reviewer most needs to check.

### Goals

End states: "X is possible", "Y no longer happens", not "build X". Stating goals as end states keeps the section about outcomes rather than about the work, and lets `Requirements` say when they have been reached.

### Non-Goals

What this change deliberately does not do, and why, whether decided at scoping or discovered during the work. This is the line that stops the change from growing, and the section most often read later: a non-goal with its reason tells the next person whether the reason still holds.

### Requirements

Statements that can be judged true or false. Together they are the stopping condition: when every one is true, the work is done, and anything further is a new change. Give each a short stable id (R1, R2, …) and never renumber; later proposals and review comments will refer to them.

A metric belongs here when the change is meant to move a number. It carries a baseline, a target and how it is measured, so that anyone can re-measure later.

### Decisions

Only decisions that had alternatives. For each: what was chosen, what was rejected, and a reason of the kind that would change if the facts changed ("we chose A because B is slower at our current volume", not "A is better"). Saying when the decision would be revisited is worth a clause. If there were no decisions with alternatives, delete the section; it is the section an assistant most easily fills with restated code.

A decision whose premise turns out to be false was never a decision. Delete it, and check what leaves the code with it.

Ids (D1, D2, …) are stable and never renumbered. When both kinds are present, the section may be split into **Product Decisions** followed by **Technical Decisions**: a decision is a product decision if reversing it changes what the team experiences or what a standard means, and a technical one if only the code changes.

### Risks

Trade-offs accepted knowingly, with the reason. Not a list of everything that could go wrong; the things that were seen, weighed, and accepted anyway. When a risk later materializes, this is the line that shows it was a choice and not an oversight.

## What stays out

A proposal does not reproduce content whose source of truth is the code, the tests or the tracker: schemas, signatures, payloads, file lists, task breakdowns. It references them by path. Copied description goes stale the day after the merge and teaches readers to distrust the document; judgment does not go stale, because it is a fact about the past.

The same rule runs the other way. The proposal is the source for the intent and judgment behind its change. A pull-request description, a tracker comment or a state document that needs that content links to the proposal rather than restating it; the same judgment written into two documents is edited apart and disagrees later. A one-sentence summary next to the link is a fine compromise; a full restatement is not.

There is no length rule. A proposal is as long as its judgment and no longer; the pressure toward brevity comes from what is excluded, not from a cap.

## Who writes it

A person writes it, or explicitly approves each of its sections before the merge. Material may come from anywhere, a design discussion, a ticket, an assistant's draft, but the text of each section is a person's judgment. How an assistant's drafts are marked, and how approval is recorded, is left to each team; [`human-ai-split`](patterns/human-ai-split.md) describes one way.

## After the merge

A merged proposal is the record of the judgment of its time. Later knowledge is better recorded in a later proposal than written over the old one: overwriting erases "why we thought so then", and anyone reading proposals as constraints, whether a person or an agent, needs to be able to tell whether one is still current. The basic practice does not enforce this. A team decides case by case until the question comes up, and [`supersession`](patterns/supersession.md) describes a way to settle it.

## What it is not

| Not a… | Because… |
|---|---|
| Product requirements document | A PRD describes a product area; a proposal describes one change, and only what code cannot say. |
| Design document or RFC | A design document describes a solution; a proposal describes the decisions inside it and points at the code for the rest. |
| Architecture decision record | An ADR holds a decision that outlives any single change; a proposal holds the decisions within one change. ([`decision-promotion`](patterns/decision-promotion.md) connects them.) |
| Pull-request description | A PR description explains a diff to its reviewer and is forgotten. A proposal is written to be found later. For changes with no behavior change, the PR description is the whole record. |
| Changelog entry | A changelog says what changed for users; a proposal says why, what was rejected, what was accepted. |
| Ticket | A ticket tracks work; a proposal holds reasoning. They link to each other. |
| Wiki page | A wiki page describes current state and is edited in place; a proposal describes one transition. |
| Session transcript | A transcript with an assistant is raw material; a proposal is what a person distilled from it. |

## Why it is shaped this way

The practice is shaped for teams that build with AI assistance, where code, summaries and verification logs are cheap to produce. That setting explains most of its choices.

- **Proportional to blast radius, not diff size.** How much a change needs documenting is set by who and what it can affect and by how hard it is to reverse. Blast radius takes judgment and diff size is free, so teams drift back to diff size unless the question is kept to one: does behavior change?
- **Judgment over description.** Describing is easier than judging, and assistants are excellent at describing. A proposal that admits description fills up with it. The six sections are all judgment, and the template refuses the rest.
- **Rides with the code.** Reviewing the change and reviewing its reasoning are one act, and the record cannot be lost separately from the code. Readers who do not live in the repository get a rendered or mirrored copy, never a moved source.
- **A record of its time.** A merged proposal says what was believed when the change was made. The cost is that current-state documents, a README, an architecture note, need their own upkeep, since the ledger of proposals will not tell a newcomer how things work today. [`living-docs-bridge`](patterns/living-docs-bridge.md) is one answer.
- **One source for the judgment.** The proposal holds its reasoning once; everything else links to it. This mirrors the other direction: the proposal does not copy what the code owns.

When two of these pull against each other in a concrete case, truth wins over cost: write the judgment down, and keep it findable by linking rather than copying.

## Going further

The practice above is complete; a team can use it alone for years. It is also deliberately silent about a great deal: how big a change must be before it needs more review, what happens to a merged proposal, what a proposal's metadata is, whether it records what was verified, how AI assistants participate, how coding agents read it, whether anything is enforced by tooling, which language it is written in.

Each of those has a candidate answer in [`patterns/`](patterns/README.md), organized by the question it answers. A team that has not adopted one is not missing it; it has not met the situation yet.
