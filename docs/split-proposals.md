# Split Change Proposals

A **Split Change Proposal** is one Change Proposal organized as two documents: **Product Requirements** and **Technical Design**. Use this form for a technically complex feature addition or change. Each document has its own purpose and can be reviewed independently. Together they describe the change the team will implement.

For small, straightforward changes, use a **Unified Change Proposal**, the original [single-document template](../templates/change-proposal.md). The [main guide](guide.md#choosing-a-form) explains how to choose between the Unified and Split forms. Splitting is useful when technical reasoning needs sustained attention of its own, such as migration, state transitions, compatibility, or architecture choices.

For a filled-in example, read the fictional note-trash [Product Requirements](../examples/2026-09-12-note-trash.requirements.md) and [Technical Design](../examples/2026-09-12-note-trash.design.md). The [examples catalog](../examples/README.md) explains how to read the pair and contrasts it with a smaller Unified proposal. These are illustrative documents, separate from the real TarkovHelper source records discussed below.

## The two parts

| Document | Answers | Review focus |
|---|---|---|
| Product Requirements | What should change, for whom, and why? What outcomes and boundaries are agreed? | Product value, observable behavior, scope, acceptance criteria, and accepted product risks |
| Technical Design | How will those requirements be met? Which mechanisms and trade-offs are sound? | Feasibility, architecture, contracts, failure behavior, verification, and migration |

Both parts belong to the same proposal. Product Requirements is complete enough for product review without tracing implementation internals. Technical Design provides enough context and reasoning for technical review, using the product requirements as its input. Independent review means distinct questions and judgments, with references between the documents where they depend on one another.

## Files and templates

Use the [Product Requirements template](../templates/product-requirements.md) and [Technical Design template](../templates/technical-design.md). For a new pair, save both under `docs/changes/` with the same date and slug:

- `YYYY-MM-DD-<slug>.requirements.md`, titled `Product Requirements: <change name>`.
- `YYYY-MM-DD-<slug>.design.md`, titled `Technical Design: <change name>`.

When splitting an existing draft, retain its `.md` path if it is already referenced, retitle it Product Requirements, and add the matching `.design.md`. Renaming it to `.requirements.md` is also an option when the clearer file name is worth updating its references.

Link each document to the other directly below its title. The titles and mutual links identify the two roles within one proposal; no third proposal, index, or summary document is needed. Repositories with established naming conventions, such as `.md` and `.spec.md`, can keep them as long as the two roles and their relationship are clear.

## What each document holds

Use the relevant sections and delete those with nothing to say. The basic meanings of Problem, Goals, Non-Goals, Requirements, Decisions, and Risks are explained in the [main guide](guide.md#what-goes-in-it).

### Product Requirements

- **Summary** states the proposed user or system outcome in a few sentences so a reviewer can understand the product change on its own.
- **Problem** describes what is wrong now, for whom, and the evidence. For user-facing work, explain the experience without implementation details.
- **Goals** states the end conditions the change should make possible.
- **Non-Goals** records what is deliberately outside the change and why.
- **Requirements** defines R1, R2, and so on as acceptance criteria that can be assessed against behavior. These are the proposal's scope and stopping condition, including necessary compatibility or performance promises.
- **Product Decisions** records product choices, rejected alternatives, reasons, and when to revisit. Use PD1, PD2, and so on for new decisions; existing IDs can be retained when splitting a draft.
- **Risks** records accepted product risks and the reason they are acceptable.

### Technical Design

- **Summary** gives the shape of the solution and the main technical ideas, making the design reviewable as its own document.
- **Non-Goals** records technical work deliberately excluded, with reasons: an adjacent refactor, a schema rewrite, or a new data source left for another change. Product Requirements keeps the product exclusions. If a technical exclusion limits the promised outcome, reflect that consequence there and link the technical rationale.
- **Context** explains relevant current behavior, technical constraints, and existing boundaries, anchored to code paths, symbols, and the commit inspected (for example, `verified at <sha>`). Identify any relevant uncommitted changes used in the analysis so the commit alone is not mistaken for the whole baseline. Distinguish confirmed causes from hypotheses.
- **Design** explains how the referenced R IDs will be met: contracts, data flow, state transitions, failure handling, and technical boundaries. Include diagrams or small contract examples when they help assess a choice. Reference executable definitions rather than copying whole schemas or file inventories.
- **Technical Decisions** records technical choices with alternatives, reasons, and revisit conditions. Use TD1, TD2, and so on for new decisions; retain existing IDs when moving decisions from a draft and qualify references with the document name.
- **Open Questions** identifies unresolved technical questions and what would settle them. Resolve questions needed to establish the agreed behavior before merging implementation; explicitly defer those outside scope.
- **Test Strategy** maps each R ID to the invariant or user-visible result to check, the test or manual method, and the expected observation. Reference existing coverage where sufficient and include important technical invariants and limits of automation. Commands to run can live here; this section is the plan, not evidence of execution.
- **Verification** records which planned checks actually ran, their observed results, and what was not checked and why. Reference the R IDs or checks in Test Strategy rather than copying the plan, and tie evidence to a run or tested revision. A command and its expected result are not a pass. While no checks have run, say so explicitly; before merge, account for the planned coverage, including any omissions or limitations.
- **Risks & Migration** records accepted technical risks, compatibility constraints, migration ordering, rollback, and relevant limitations. Link the corresponding product consequence rather than copying its rationale.

## Keep the pair connected

Each requirement has one definition in Product Requirements. Technical Design references its R ID in Design and Test Strategy; Verification records the results against that planned coverage. If a technical constraint changes what users receive, what is in scope, or when the work is done, revise Product Requirements too.

Each decision's rationale also has one home. Product Requirements explains a product choice; Technical Design explains a technical choice. Where one affects the other, summarize the consequence and link to the decision. Qualify IDs with document links when referring to another proposal.

The pair describes one bounded change. Task ordering and live progress belong in the plan, PR, or tracker. Technical Design records the proposed solution and its reasons; after merge, code and maintained reference documents describe the system today.

## Review each aspect, then check the pair

The same person can perform all three passes, or reviewers can divide them by expertise. The distinction is what each review evaluates, not a required set of roles or approval fields.

| Review | Questions to settle |
|---|---|
| Product review | Is the problem supported by evidence? Are the proposed behavior and scope worthwhile? Are acceptance criteria observable and product trade-offs acceptable? |
| Technical review | Does the design have a plausible way to meet the referenced requirements? Can its assumptions be checked against the inspected revision? Are technical exclusions justified, and are failure paths, compatibility, rollback, and the test strategy sufficient? |
| Consistency review | Does every R ID have design and planned test coverage? Does the design respect both documents' Non-Goals? Are product consequences of technical risks reflected in Product Requirements? Do any decisions or unresolved questions contradict the agreed scope? Once checks run, does Verification account for the plan and its limits? |

Review product intent without requiring a tour of implementation details. Review the design against the referenced requirements without silently changing those requirements. If either review exposes a constraint that changes the other document, revise it and revisit the affected judgments. Recheck the pair after material revisions so earlier reviews do not stand in for review of a changed proposal.

There is no fixed waterfall of approvals. Investigation and review can iterate in either direction. Agreement with one document alone does not establish that the whole proposal is coherent, and a completed design review is not evidence that implementation or verification has finished.

## Starting with one document and splitting later

Start with the Unified form when the original template is enough. If technical complexity emerges, convert the draft to the Split form:

1. Retitle the single document Product Requirements. Keep its existing `.md` path when preserving references is useful; renaming it to `.requirements.md` is optional.
2. Keep the problem, goals, scope, and R IDs there. Move technical choices and technical risks into a new `<same-date-and-slug>.design.md`; retain meaningful alternatives and reasons.
3. Keep existing R and decision IDs stable. Use PD or TD IDs for new decisions. Update references to moved decisions where possible; when an existing review comment still points to the old location, leave a short link under the original ID there. Keep the rationale only in the destination document.
4. Add mutual links, and update affected references if a path or heading changed. Fill the technical Non-Goals, inspected Context, Design, and Test Strategy; record Verification as checks run. Perform the two reviews and consistency check.

The original draft becomes the product part of the pair, at either its retained path or its new name. Keep one copy of it; a third overview would duplicate the proposal. Git retains the drafting history. This conversion is for work in progress, not a reason to rename or retrofit merged historical proposals.

Revise both drafts into a coherent account as evidence changes. Preserve meaningful reversals and their reasons in the relevant Decisions section while updating the design to agree. An implementer should be able to follow the current proposal without reconstructing it from contradictory draft paragraphs.

## Merging and later changes

Finish both documents with the implementation and merge them in the same PR as the work they cover. The PR body links to both parts of the proposal. Record the verification actually performed and any limitations before merge.

After merge, preserve the reasoning of the time. A later change records its own judgment and links to the decisions it reverses. A short `Superseded in part by <document>: <affected decisions>` note on the older record can make that relationship discoverable in both directions; add it with the later change and leave the original rationale intact. The documents need no ongoing status or progress fields.

### Work spanning several PRs

Prefer one proposal, in either form, per independently deliverable change. An optional direction document can explain shared constraints and the division of a larger program. Explicitly state when it records direction whose implementation is deferred: merging that direction does not mean the program has shipped.

If an existing proposal already spans several PRs, identify the deferred scope rather than letting the first merge imply completion, and link the later work to it. Individual implementation proposals can link back to shared direction while giving completion criteria for their own PRs. Keep live progress in PRs or issues.

## From TarkovHelper's decision docs

TarkovHelper's [process record][process] explains why it separated product decisions from technical design and removed fields whose updates had been missed. Its [versioned data channel PRD][channel-prd] states user requirements while the [sibling spec][channel-spec] develops channel contracts, integrity checks, and publishing behavior. The [Seasonal Profile spec][seasonal] maps R1-R5 to verification. These source documents demonstrate the separation; they do not establish that this exact form and review guidance have already been used there.

This compact example adapts the channel pair's R6 and download-verification design. It illustrates the two review perspectives and their connection, not a new implementation record or an executed test report.

| Location | Example content | Review question |
|---|---|---|
| Product Requirements, Requirements | R6: Reject a download that disagrees with its published metadata and keep the working data. | Is retaining working data the right user guarantee? |
| Technical Design, Design | For R6, validate the temporary download before replacing the working database or advancing the local version bookmark. | Can a failure leave either the data or bookmark in an inconsistent state? |
| Technical Design, Technical Decisions | TD1: Put the digest and version in one manifest; a separate digest file can be cached independently. Revisit if publication guarantees an atomic snapshot across files. | Does the chosen mechanism address the mismatch and the rejected alternative's failure mode? |
| Technical Design, Test Strategy | For R6, supply mismatched metadata and assert that the database and bookmark stay unchanged, then try a valid download. | Would the planned check establish both preservation and the ability to recover on a later attempt? |

This illustration has no executed Verification result. In an implementation record, Verification identifies which planned checks ran, the tested revision, the observations, and any checks not run with their reasons.

Some source conventions are adapted. Here the Unified and Split forms are both complete Change Proposals; these form names are this practice's vocabulary, not names taken from TarkovHelper. Explicit file suffixes are recommended for new pairs; existing paths and IDs can stay when splitting a draft. Drafts can be revised into a coherent account; the source describes them as append-only. TarkovHelper's [roadmap spec][roadmap] provides a useful example of explicit deferred implementation, while the [quest-data handoff][handoff] shows why expected verification results need to be distinguished from observed results.

Experience in use should test whether separate reviews help expose different kinds of mistakes, whether references make consistency review practical, and when two documents add effort without improving the proposal. Use the Unified form for later changes that do not need this separation.

[process]: https://github.com/josephjang/TarkovHelper/blob/425ac5546432667520f5c1378df5510b9fc7c5e1/docs/decisions/feature-decision-docs-process.md
[channel-prd]: https://github.com/josephjang/TarkovHelper/blob/425ac5546432667520f5c1378df5510b9fc7c5e1/docs/decisions/feature-versioned-data-channel.md
[channel-spec]: https://github.com/josephjang/TarkovHelper/blob/425ac5546432667520f5c1378df5510b9fc7c5e1/docs/decisions/feature-versioned-data-channel.spec.md
[seasonal]: https://github.com/josephjang/TarkovHelper/blob/425ac5546432667520f5c1378df5510b9fc7c5e1/docs/decisions/feature-seasonal-profile.spec.md#test-strategy
[roadmap]: https://github.com/josephjang/TarkovHelper/blob/425ac5546432667520f5c1378df5510b9fc7c5e1/docs/decisions/feature-eft-1-1-roadmap.spec.md
[handoff]: https://github.com/josephjang/TarkovHelper/blob/425ac5546432667520f5c1378df5510b9fc7c5e1/docs/assessments/2026-08-quest-data-1-1-refresh-handoff.md#read-this-first
