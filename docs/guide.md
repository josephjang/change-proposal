# Change Proposals

This is the practice, explained once. It is written to be understood rather than enforced, and where it is unsure it says so.

## What a change proposal is

A **change proposal** records the intent and judgment behind one change to a product or system: why it is being made, what it deliberately leaves out, what was decided and what was rejected, and what risks were knowingly accepted. It is started before the work and finished with it: whoever builds the change, a person or an AI assistant, builds it from the proposal, and after the merge the proposal is the change's record. A person or an assistant writes it; what stands behind what it says is the process the change goes through, review included. It lives in the repository and merges in the same pull request as the change.

Four things make it what it is. They follow from the setting it is made for: teams that build with AI assistance, where code, summaries and verification logs are cheap to produce and judgment is not.

- **It is what the change is built from.** It comes before the code, not after it, and whoever implements the change, a person or an AI assistant, works from it: `Problem` says why, `Goals` the end state, `Non-Goals` what not to build, `Requirements` when to stop, `Decisions` which way was chosen. A proposal that could not be handed to an implementer is missing something.
- **It holds judgment, not description.** Code, schemas and interfaces describe themselves, and copied description goes stale the day after the merge. A proposal holds what the code cannot recover: the reasons.
- **It travels with the change.** Same repository, same pull request, same review, same history. A document that must be found somewhere else is not read, by people or by agents.
- **It is small.** Six sections and an optional summary. Anything that would make it larger is either description, which belongs in the code, or an addition for a situation this practice does not cover (see [Going further](#going-further)).

### Why "proposal"

The document's first job is to put an intent in front of whoever will build the change and whoever will review it, and, unlike a spec, it does not try to describe the solution. It proposes: here is the problem, here is what we will not do, here is what we decided and gave up. After the merge it is still called a proposal; its position on the main branch says it was carried out.

## When to write one

Write a proposal when a change alters observable behavior. Skip it when it does not: a refactor with identical behavior, a typo, a dependency patch, tests only. In that case the pull-request description says there is no behavior change and how that was checked.

That is the only sizing question, and it is answered by looking at what the change *does*, never at how many lines it touches, how long it took, or whether a person or an assistant wrote the code. A 2,000-line mechanical refactor with identical behavior needs no proposal. A one-line change to a permission check needs one. Diff size correlates badly with risk, and the correlation collapses entirely once assistants produce thousands of correct mechanical lines in minutes.

## Where it lives

`docs/changes/YYYY-MM-DD-<slug>.md`, committed in the same pull request as the code. A repository with its own document location or naming convention uses that instead; what matters is that the proposal is found next to the code, not the exact path.

The title is `Change Proposal: <change name>`, so that the document says what it is to a reader who never sees its path. A repository that already marks its documents its own way, with an id scheme or a date, uses that marker instead.

## What goes in it

A title, an optional summary, and six sections with fixed names, in this order (the [template](../templates/change-proposal.md) carries them all):

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

Optional. Useful when the proposal is long enough that a reader wants the shape before the detail; delete it when the proposal is short enough to speak for itself.

### Problem

What is wrong right now, for whom, and the evidence: an issue, a metric, a request. Where it matters, how it works today and why it was built that way; the diff shows only "after", and the reason for the old shape is exactly what the next person will not be able to recover.

`Problem` is not "what we will build". A proposal that starts from a solution has skipped the part a reviewer most needs to check.

### Goals

End states: "X is possible", "Y no longer happens", not "build X". Stating goals as end states keeps the section about outcomes rather than about the work, and lets `Requirements` say when they have been reached.

### Non-Goals

What this change deliberately does not do, and why, whether decided at scoping or discovered during the work. This is the line that stops the change from growing, and the section most often read later: a non-goal with its reason tells the next person whether the reason still holds.

### Requirements

Statements that can be judged true or false. Together they are the stopping condition for whoever implements the change, a person or an assistant: when every one is true, the work is done, and anything further is a new change. Give each a short id (R1, R2, …) so that review comments and later proposals can refer to it.

A metric belongs here when the change is meant to move a number. It carries a baseline, a target and how it is measured, so that anyone can re-measure later.

### Decisions

Only decisions that had alternatives. For each: what was chosen, what was rejected, and a reason of the kind that would change if the facts changed ("we chose A because B is slower at our current volume", not "A is better"). Saying when the decision would be revisited is worth a clause. If there were no decisions with alternatives, delete the section; it is the section an assistant most easily fills with restated code.

### Risks

Trade-offs accepted knowingly, with the reason. Not a list of everything that could go wrong; the things that were seen, weighed, and accepted anyway. When a risk later materializes, this is the line that shows it was a choice and not an oversight.

## What stays out

A proposal does not reproduce content whose source of truth is the code, the tests or the tracker: schemas, signatures, payloads, file lists, task breakdowns. It references them by path. Copied description goes stale the day after the merge and teaches readers to distrust the document; judgment does not go stale, because it is a fact about the past.

The same rule runs the other way. The proposal is the source for the intent and judgment behind its change. A pull-request description, a tracker comment or a state document that needs that content links to the proposal rather than restating it; the same judgment written into two documents is edited apart and disagrees later. A one-sentence summary next to the link is a fine compromise; a full restatement is not.

There is no length rule. A proposal is as long as its judgment and no longer; the pressure toward brevity comes from what is excluded, not from a cap.

## After the merge

A merged proposal is the record of the judgment of its time. Later knowledge is better recorded in a later proposal than written over the old one: overwriting erases "why we thought so then", and anyone reading proposals as constraints, whether a person or an agent, needs to be able to tell whether one is still current. The practice does not enforce this; a team decides case by case until the question comes up.

A ledger of proposals will not tell a newcomer how things work today. Current-state documents, a README or an architecture note, need their own upkeep.

## What it is not

| Not a… | Because… |
|---|---|
| Product requirements document | A PRD describes a product area; a proposal describes one change, and only what code cannot say. |
| Design document or RFC | A design document describes a solution; a proposal describes the decisions inside it and points at the code for the rest. |
| Architecture decision record | An ADR holds a decision that outlives any single change; a proposal holds the decisions within one change. |
| Pull-request description | A PR description explains a diff to its reviewer and is forgotten. A proposal is written to be found later. For changes with no behavior change, the PR description is the whole record. |
| Ticket | A ticket tracks work; a proposal holds reasoning. They link to each other. |
| Prompt or session transcript | A prompt is written for one session and lost with it, and a transcript is raw material; a proposal is what the prompt points at and what the transcript was distilled into, reviewed with the code and kept. |

## Going further

That is the whole practice. It says nothing, on purpose, about review stages, metadata, whether a proposal records what was verified, how an assistant's drafts are approved, what coding agents read, tooling, or the language it is written in. A team that meets a situation the practice does not cover writes the smallest addition that answers it, as a **pattern**: optional, adopted when its situation appears, and dropped without touching what was written. The practice never assumes one, and none is published here yet; a team that writes one is welcome to send it here with what it learned.
