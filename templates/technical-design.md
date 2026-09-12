# Technical Design: [Change name]

<!-- Technical part of a Split Change Proposal, paired with Product Requirements.
     Save as docs/changes/YYYY-MM-DD-<slug>.design.md, or use the repo's convention.
     Add a relative link to the actual Product Requirements file directly below this title;
     it may retain its original .md path or use .requirements.md, and it links back.
     Both documents together are the proposal. There is no third summary or proposal file.
     Explain enough context and reasoning for a dedicated technical review.
     Refer to the Product Requirements' R IDs without redefining acceptance criteria.
     Revise drafts and preserve meaningful reversals and reasons in Technical Decisions.
     Merge both documents with their implementation. Explicitly state any deferred implementation.
     Delete sections with nothing to say. Full explanation and separate review questions:
     https://github.com/josephjang/change-proposal/blob/main/docs/split-proposals.md -->

## Summary

<!-- The solution in a few sentences and the main technical ideas, readable on its own. -->

## Non-Goals

<!-- Technical work deliberately excluded, and why: an adjacent refactor, a schema rewrite,
     or a new data source left for another change. Product exclusions stay in Product Requirements.
     Reflect any consequence for the promised outcome there and link the technical rationale. -->

## Context

<!-- Relevant current behavior, technical constraints, and boundaries, anchored to paths
     and symbols. Record the inspected commit (for example, "verified at <sha>") and identify
     any relevant uncommitted changes used in the analysis. Distinguish confirmed root causes
     from hypotheses. -->

## Design

<!-- Connect the design to R IDs from Product Requirements. Explain boundaries, contracts,
     data flow, state transitions, and failure behavior needed to assess the choices.
     Use a diagram or small contract example when useful. Reference executable definitions;
     omit whole schemas, exhaustive file lists, and task breakdowns. -->

## Technical Decisions

<!-- Record technical choices with alternatives. Link product decisions rather than repeating them.
     Use TD IDs for new decisions; retain existing IDs when moving decisions from a draft and
     update references or leave a short pointer at the old location where needed.
     If a choice changes scope, a user promise, or the stopping condition, revise Product
     Requirements too. Keep meaningful reversals here while updating Design to agree. -->

- **TD1: [Decision sentence.]** [Rejected alternative, reason, and when to revisit.]

## Open Questions

<!-- What remains unresolved and what would settle it. Resolve questions needed to establish
     the agreed behavior before merging implementation; explicitly defer those outside scope. -->

## Test Strategy

<!-- Account for every R ID with a check and the observable result that proves it.
     Reference existing coverage where sufficient; include important technical invariants,
     manual checks, and their limits. Add commands when useful.
     This is the plan: method and expected observation, not a record of a passing run. -->

- R1: [Invariant or behavior; test or manual method; expected observation.]

## Verification

<!-- Record which planned checks actually ran and what was observed, tied to a run or tested
     revision. Reference R IDs or checks from Test Strategy rather than copying the plan.
     Say what was not checked and why. If no checks have run yet, say so explicitly.
     Before merge, account for the planned coverage, including omissions and limitations. -->

- Checked: [R IDs or checks; run or tested revision; observed results.]
- Not checked: [Check; reason; remaining limitation.]

## Risks & Migration

<!-- Accepted technical risks and why, including compatibility, migration ordering, rollback,
     and limitations. Reflect product consequences in Product Requirements and link them.
     Independent technical review and the pair's consistency review should assess these links. -->
