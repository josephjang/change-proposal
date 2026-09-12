# Change Proposals

This is the practice, explained once. It is written to be understood rather than enforced, and where it is unsure it says so.

## What a change proposal is

A **Change Proposal** records the intent and judgment behind one change to a product or system: why it is being made, what it deliberately leaves out, what was decided and what was rejected, and what risks were knowingly accepted. It is started before the work and finished with it: whoever implements the change works from the proposal, and after the merge the proposal is the change's record.

A proposal has two named forms. A **Unified Change Proposal** keeps the change in one concise document. A **Split Change Proposal** separates it into **Product Requirements** and **Technical Design**, together one proposal. The Unified form suits small, straightforward feature additions and changes. The Split form suits technically complex changes whose product and technical aspects need separate treatment and review.

A person or an assistant writes it; what stands behind what it says is the process the change goes through, review included. It lives in the repository and merges in the same pull request as the change.

Four things make it what it is. They follow from the setting it is made for: teams that build with AI assistance, where code, summaries and verification logs are cheap to produce and judgment is not.

- **It is what the change is built from.** It comes before the code. It tells the implementer why, what end state to reach, what not to build, when to stop, and which choices matter. A technically complex change also has a design that can be assessed against those requirements.
- **It keeps the reasoning.** Code describes the implemented system; the proposal preserves the reasons, rejected alternatives, and accepted risks that code cannot recover. Technical Design explains the proposed solution far enough to review those choices without becoming a copy of the implementation.
- **It travels with the change.** Same repository, same pull request, same review, same history. Both documents in the Split form belong to that change.
- **Its form fits the work.** The original six-section document keeps ordinary changes simple. Separating Product Requirements and Technical Design gives complex changes room for independent review without making every change pay that cost.

### Why "proposal"

The proposal's first job is to put the intended change in front of whoever will build it and whoever will review it. It explains the problem, the scope, the choices, and the trade-offs. When the solution needs its own technical treatment, Technical Design is part of that proposal. After the implementation merges, it is still called a proposal; it records what the change was built from.

## When to write one

Write a proposal when a change alters observable behavior. Skip it when it does not: a refactor with identical behavior, a typo, a dependency patch, tests only. In that case the pull-request description says there is no behavior change and how that was checked.

That decides whether a proposal is needed, and it is answered by looking at what the change *does*, never at how many lines it touches, how long it took, or whether a person or an assistant wrote the code. A 2,000-line mechanical refactor with identical behavior needs no proposal. A one-line change to a permission check needs one.

## Choosing a form

Use **Unified form** and **Split form** as the short names. They describe how one proposal is organized, not size tiers, approval levels, or stages of work. Both are complete proposals. A Unified proposal is not a product-only draft awaiting a design, and either document alone is not a complete Split proposal. A change can start in either form; moving from Unified to Split is a reorganization when needed, not a required progression.

| Form | Use it for | Documents |
|---|---|---|
| Unified | Small, straightforward changes whose requirements and main decisions are enough to build and review from | One document, using the original [Change Proposal template](../templates/change-proposal.md) |
| Split | Changes with technical complexity that benefits from separate product and technical review | Two documents, [Product Requirements](../templates/product-requirements.md) and [Technical Design](../templates/technical-design.md), together one proposal |

Use the Unified form as the starting point for ordinary work. Choose the Split form when the technical aspect needs its own explanation: interacting state transitions, a data migration, compatibility across components, or a consequential architecture choice. A small feature can contain one of these; file count or a fixed line threshold would miss it.

The split lets a reviewer assess whether the desired behavior and scope are right, and separately assess whether the design is sound. One person can do both reviews in separate passes. Finish by checking that the two documents agree. This does not prescribe a fixed sequence of approvals: technical investigation can change the product proposal too.

The [Split form guide](split-proposals.md) explains each document, the review questions, and how to split a draft when complexity becomes clear during the work. The Unified form remains sufficient when a separate design review would add little.

The [worked examples](../examples/README.md) show both forms filled in for independent changes to the same fictional notes app: clearing a search in one document, and adding recoverable note deletion in two.

## Where it lives

Use `docs/changes/`, with the proposal committed in the same pull request as the code. These are the recommended names when starting a new proposal:

| Form or part | File | Title |
|---|---|---|
| Unified proposal | `YYYY-MM-DD-<slug>.md` | `Change Proposal: <change name>` |
| Product part of a Split proposal | `YYYY-MM-DD-<slug>.requirements.md` | `Product Requirements: <change name>` |
| Technical part of that Split proposal | `YYYY-MM-DD-<slug>.design.md` | `Technical Design: <change name>` |

The form names are vocabulary for discussion and guidance, not new file names, title prefixes, or metadata fields. The original template is the Unified template without being renamed. In the Split form, each document's title continues to identify its product or technical role.

The two files share a date and slug and link to each other. When splitting an existing draft, its `.md` path can stay: retitle that file Product Requirements and add the matching `.design.md`. Existing requirement and decision IDs can stay too; update references to content that moves. The [conversion guide](split-proposals.md#starting-with-one-document-and-splitting-later) explains the details.

No third proposal or summary file is needed. A repository with its own document location, naming convention, or title marker can use that instead; what matters is that the proposal is identifiable and found next to the code.

## What goes in it

In the Unified form, use a title, an optional summary, and six sections with fixed names, in this order (the [original template](../templates/change-proposal.md) carries them all):

| Section | Holds |
|---|---|
| **Summary** (optional) | Three to five sentences directly under the title: what changes, why, what does not change. |
| **Problem** | What is wrong now, for whom, with the evidence. |
| **Goals** | The end states the change makes possible. |
| **Non-Goals** | What the change deliberately does not do, and why. |
| **Requirements** | Statements that can be judged true or false; when all are true, the work is done. |
| **Decisions** | Decisions that had alternatives: what was chosen, what was rejected, why. |
| **Risks** | Trade-offs accepted knowingly, with the reason. |

The names are fixed and in English so that this form reads consistently across repositories, and so that tooling and agents can find sections without guessing. The Split form uses the [Product Requirements and Technical Design sections](split-proposals.md#what-each-document-holds); the six-section layout applies to the Unified form.

A section with nothing to say is deleted rather than filled: an empty heading tells the reader nothing, and a section filled for form teaches them to skip it next time. In practice that means `Decisions`, `Risks` and the optional `Summary`. A change worth a proposal always has a problem, a goal, something it will not do, and a way to tell when it is done.

Each section, in more detail:

### Summary

Optional. Useful when the proposal is long enough that a reader wants the shape before the detail; delete it when the proposal is short enough to speak for itself.

### Problem

What is wrong right now, for whom, and the evidence: an issue, a metric, a request. Where it matters, how it works today and why it was built that way; the diff shows only "after", and the reason for the old shape is exactly what the next person will not be able to recover.

`Problem` is not "what we will build". A proposal that starts from a solution has skipped the part a reviewer most needs to check.

### Goals

End states: "X is possible", "Y no longer happens", not "build X". Stating goals as end states keeps the section about outcomes rather than about the work, and lets `Requirements` say when they have been reached.

### Non-Goals

What this change deliberately does not do, and why, whether decided at scoping or discovered during the work. This is the line that stops the change from growing, and the section most often read later: a non-goal with its reason tells the next person whether the reason still holds.

### Requirements

Statements that can be judged true or false. Together they are the stopping condition for whoever implements the change, a person or an assistant: when every one is true, the work is done, and anything further is a new change. Give each a short id (R1, R2, ...) so that review comments and later proposals can refer to it.

A metric belongs here when the change is meant to move a number. It carries a baseline, a target and how it is measured, so that anyone can re-measure later.

### Decisions

Only decisions that had alternatives. For each: what was chosen, what was rejected, and a reason of the kind that would change if the facts changed ("we chose A because B is slower at our current volume", not "A is better"). Saying when the decision would be revisited is worth a clause. If there were no decisions with alternatives, delete the section; it is the section an assistant most easily fills with restated code.

### Risks

Trade-offs accepted knowingly, with the reason. Not a list of everything that could go wrong; the things that were seen, weighed, and accepted anyway. When a risk later materializes, this is the line that shows it was a choice and not an oversight.

## What stays out

The Unified form focuses on intent and judgment. It references code, tests, and tracker content by path instead of reproducing schemas, signatures, payloads, file lists, or task breakdowns.

In the Split form, Technical Design can explain a proposed contract, state transition, or data flow when a choice depends on it. Include enough to assess the design before implementation, then reference executable definitions once they exist. Copied implementation detail goes stale; the design remains a record of the reasoning for that change, not a maintained description of the current system.

The proposal is the source for the intent and judgment behind its change. In the Split form, Product Requirements owns scope, requirements, and product judgments; Technical Design owns detailed technical judgments, design, and verification. Each requirement or rationale has one authoritative home, linked from the other document.

A pull-request description, tracker comment, or state document that needs that content links to its source rather than restating it. A one-sentence summary next to the link is a fine compromise; a full restatement is not.

There is no length rule. Include what the reader needs to assess the change's intent and choices, with technical design where needed; the pressure toward brevity comes from what is excluded, not from a cap.

## After the merge

A merged proposal is the record of the judgment of its time, whether it consists of one document or two. Later knowledge is better recorded in a later proposal than written over the old one: overwriting erases "why we thought so then". Anyone reading proposals as constraints needs to be able to tell whether a later change reversed a decision. The practice does not enforce this; a team decides case by case until the question comes up.

A ledger of proposals will not tell a newcomer how things work today. Current-state documents, a README or an architecture note, need their own upkeep. For work spanning several PRs, distinguish shared direction from implemented changes as described in [Work spanning several PRs](split-proposals.md#work-spanning-several-prs).

## Relationship to other documents

Product Requirements and Technical Design can be constituent documents of a Change Proposal. Each concerns the same bounded change: the product part explains what should change and why, and the technical part explains how the requirements will be met and verified.

| Document | Relationship |
|---|---|
| Architecture decision record | An ADR holds a decision that outlives any single change; a proposal holds the decisions within one change. |
| Pull-request description | A PR description explains a diff to its reviewer and points to the proposal for the lasting reasoning. For changes with no behavior change, the PR description can be the whole record. |
| Ticket | A ticket tracks work; a proposal holds reasoning. They link to each other. |
| Prompt or session transcript | A prompt can point to the proposal, and a transcript supplies raw material. The proposal distills the reviewed intent and judgment into a record kept with the code. |
| Reference document | A reference document describes the current system and needs upkeep. A proposal records a particular change and the judgment of its time. |

## Going further

These two forms describe the core practice. Teams choose their own approval ownership, agent instructions, tooling, and language conventions. A team that meets a situation the practice does not cover writes the smallest addition that answers it, as a **pattern**: optional, adopted when its situation appears, and dropped without touching what was written.

The [Split form guide](split-proposals.md) develops the form for technically complex changes with templates and examples from TarkovHelper. Other extensions can be contributed with the situation that called for them and what the team learned in use.
