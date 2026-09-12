# Change Proposal: Two forms for ordinary and technically complex changes

## Summary

A Change Proposal has two named forms: Unified keeps the change in one concise document; Split separates Product Requirements and Technical Design into two documents. Small, straightforward changes use the Unified form with the original single-document template. Technically complex changes use the Split form so each aspect can be written and reviewed on its own, with a consistency review connecting the pair. Both are complete proposals; the names describe organization, not levels of rigor or stages of work. Technical Design distinguishes technical scope, the inspected baseline, planned tests, and observed verification; splitting a draft can preserve existing paths and IDs.

## Problem

The initial practice defines a Change Proposal as a single document focused on intent and judgment. That works for ordinary feature additions and changes, but a technically complex feature also needs enough design to assess feasibility, failure behavior, compatibility, or migration. Combining those details with product requirements makes it harder to review either aspect independently.

TarkovHelper has met this situation. Its decision docs separate product requirements from technical design for changes such as versioned data channels and seasonal profiles. The [Split form guide](../split-proposals.md#from-tarkovhelpers-decision-docs) identifies the source records and the limits of this adaptation. Change-proposal needs a clear way to represent both documents as one proposal while keeping the original concise form available.

Authors and reviewers also need short, stable names for discussing which form to use. Calling only the single-document form a "Change Proposal" would confuse one form with the concept that includes both.

## Goals

- Small feature additions and changes remain workable from the original single-document proposal.
- Technically complex changes have distinct product and technical documents that can be reviewed independently.
- Both forms retain one scope and one coherent account of requirements, decisions, and accepted risks.
- An author can split a draft when technical complexity becomes clear without creating duplicate requirements or losing earlier reasoning.
- Authors and reviewers can name either form without restating its document structure or implying that one is incomplete.
- Readers can see both forms filled in for realistic changes, with fictional examples distinguished from actual implementation records.

## Non-Goals

- Requiring two documents for every change or choosing by line count.
- Introducing a third summary document for the two-document form.
- Changing the behavior-change trigger, importing approval gates or tooling, or changing TarkovHelper.
- Rewriting historical proposals or introducing a roadmap template.
- Renaming existing files or changing document title conventions to carry a form label, or adding form metadata.

## Requirements

- R1: The README and guide define Change Proposal as the whole proposal, Unified Change Proposal as its single-document form, and Split Change Proposal as its Product Requirements and Technical Design pair.
- R2: The original single-document template and initial-release record remain unchanged; small, straightforward changes can continue using that template alone.
- R3: The Split form consists of Product Requirements and Technical Design, with separate templates, recommended file names for new pairs, mutual links, and no third proposal document. Converting a draft can retain its existing path and decision IDs.
- R4: Product and technical review each have a stated scope. A final consistency review checks requirement coverage, scope, risks, and unresolved questions across the pair without requiring a fixed approval sequence.
- R5: Requirements and decision rationales each have one authoritative home. Technical Design references the Product Requirements' R IDs in design and test strategy, with executed results recorded in Verification; product consequences of technical choices are reflected in Product Requirements.
- R6: The guide explains how to move from a single draft to two documents, preserve reasons while revising drafts, and distinguish merged direction from completed implementation across multiple PRs.
- R7: Every template section is explained, links resolve, and source examples are attributed to an inspected revision without claiming this exact adaptation has already been used.
- R8: Technical Design has separate Non-Goals, Test Strategy, and Verification sections. Context identifies the inspected commit and any relevant uncommitted changes, so a reviewer can recover the basis of the design.
- R9: The guide explains the short names Unified form and Split form, and distinguishes them from size tiers, approval levels, or stages of work. The Split form guide and its two template instruction comments use the new terminology without changing the component names or their responsibilities.
- R10: Form names do not rename existing files, change document title conventions or section layouts, or introduce metadata fields.
- R11: Published examples show a complete Unified proposal and a mutually linked Split pair for independent changes to the same fictional app. English is the default, with matching Korean .ko.md editions that preserve requirement and decision IDs, same-language pairing, and language-switch links. The README and guides link to them, and the examples distinguish assumed product behavior and planned tests from inspected code and observed results.

## Decisions

- **D1: Treat both forms as Change Proposals.** A technical attachment to a document still called the whole proposal was considered, but it leaves the technical half looking secondary and the term ambiguous. In the Split form, Product Requirements and Technical Design are peer documents within one proposal. The Unified form remains the default for small, straightforward changes. Revisit if the distinction makes ordinary work harder to explain.

- **D2: Use separate product and technical reviews, followed by a consistency review.** Requiring reviewers to assess both aspects in one undifferentiated pass obscures whether a concern is about the desired behavior or the proposed implementation. Independent review can be done by different people or by one person in separate passes. Technical discoveries can change product requirements, so a fixed waterfall of approvals is not prescribed. Revisit if teams need a separate workflow for approval ownership.

- **D3: Recommend matching .requirements.md and .design.md suffixes for new pairs, while retaining established paths and IDs during conversion.** Requiring the existing product draft to be renamed was considered first because symmetric names reveal both roles. It was relaxed after review: a title and mutual links identify the roles without breaking a path already used by review comments. A single draft can become Product Requirements at its existing .md path with a sibling .design.md; existing D IDs can remain when decisions move, with references or short pointers connecting them. New decisions can use PD and TD IDs. A third index document was rejected because two mutually linked files already identify the proposal.

- **D4: Split responsibility and keep one definition of each claim.** Product Requirements owns outcomes, scope, acceptance criteria, product decisions, and product risks. Technical Design owns detailed technical choices, mechanisms, verification, and migration risks. Copying requirements or rationale into both documents makes independent revisions disagree. Revisit if cross-references prevent a reviewer from understanding the consequences of a decision.

- **D5: Extend the core definition while preserving the original form.** The [initial release's D1](2026-08-30-initial-release.md#decisions) centered the practice on one six-section document. Two forms now belong in the core explanation because choosing how to represent the proposal is fundamental to its use. Optional additions for other situations can still be patterns; this change does not publish a catalog of speculative extensions. The initial-release proposal remains the historical account of the earlier definition.

- **D6: Revise drafts into a coherent design and preserve meaningful reversals in Decisions.** Applying the source project's append-only convention during drafting would leave obsolete assumptions competing with the current proposal. After merge, preserve the reasoning of the time and record later judgment in later proposals. A document covering deferred implementation says so explicitly; a first merge does not establish that later work shipped. Revisit if important reasoning is routinely lost during revisions.

- **D7: Give technical exclusions, planned tests, and observed results distinct places.** The earlier draft put technical boundaries in Design and test plans and results in Verification. Separate Non-Goals and Test Strategy sections make the technical review's scope and intended evidence easier to find; Verification then records only what actually ran or was not checked. Context records the inspected commit, and any relevant uncommitted changes, so the design's starting assumptions can be revisited. The source project's specs use these distinctions, and the cross-worktree review made their value clearer. Revisit if authors repeatedly duplicate content across these sections rather than reference it.

- **D8: Name the forms Unified and Split.** These describe whether the change's intent and decisions are held in one document or separated by product and technical responsibility. Simple/Complex would label the change rather than its organization; Lite/Full would imply that one form is incomplete. Single-document/Two-document remain useful descriptions, but the named concepts make discussion shorter. Revisit if readers consistently mistake Unified for combining several changes or Split for separate proposals.

- **D9: Keep form names separate from document names.** A Unified proposal still uses the title `Change Proposal`; a Split proposal still has `Product Requirements` and `Technical Design` titles. New prefixes, template file names, or a form field would add migration work without improving the distinction. The guide identifies the unchanged original template as the Unified template.

- **D10: Publish fictional worked examples under examples/, separate from actual change records.** Templates alone show the headings but not how much reasoning each form needs. Keeping samples temporary would make them hard for later readers to find; putting them under docs/changes/ would suggest that this repository implements the fictional features. One catalog compares the forms without adding a third document to the Split proposal. Both examples use the same fictional app but independent changes, so they do not imply a required Unified-to-Split progression. English default files and Korean .ko.md editions make the same examples accessible in both languages; they share IDs and are updated together rather than treated as separate proposals. Revisit if readers still mistake illustrative assumptions or test plans for verified implementation facts.

## Risks

- The Split form costs more to author and review. Accepted when technical complexity makes separate treatment useful; the Unified form remains sufficient for straightforward changes.
- Independent reviews can miss a mismatch between what is wanted and what is designed. Accepted with explicit requirement references and a consistency review after either side changes materially.
- The source project demonstrates the value of separation, but this adaptation's naming and review guidance still need experience in use. Accepted with attributed examples and an explicit request for feedback from real changes.
- Readers could mistake the two names for sequential stages. Accepted with an explicit explanation that a change may start in either form and need not move from Unified to Split.
