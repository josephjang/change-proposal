# Change Proposal: Initial release of the change-proposal practice

## Problem

Teams that build with AI assistants produce code faster than they record why. What the assistant built from was a prompt, written for one session and lost with it, and the intent and judgment behind the change — what was rejected, what was knowingly accepted, what was actually verified — is lost in a chat transcript or written into a document away from the code that the next person or agent never reads. Existing document types (PRDs, design docs, ADRs) each cover part of this; none is sized for an ordinary change; and single prescribed processes get adopted whole and abandoned as ceremony, or adopted in part with the reasoning for the skipped parts lost.

## Goals

- A team can start recording the intent and judgment behind its changes with one template and one short document to read, and nothing else.
- A proposal is enough for whoever implements the change, a person or an AI assistant, to build it from: it says why, what end state, what not to build, when the work is done, and which way was chosen.
- What the practice asks for can be understood in one sitting, with the reason next to each ask, so that a team adapting it can tell what to keep.
- The practice grows for a team without changing what is described here: a team that meets a situation it does not cover writes a pattern for it, adopts it, and drops it without touching what was written; changing the practice itself is a separate change, recorded like any other (D5).

## Non-Goals

- Shipping tooling (lint, skills, a config format): nothing in the practice is enforced by a machine, and what a machine should check is not known until adoptions agree on what has stopped changing (D2, D3).
- Translating the practice's documents: English is the single source. How a team writes its proposals in another language is that team's to settle.
- Publishing patterns ahead of the situations that call for them: none is published until an adoption has met the situation it answers (D4).
- A worked example repository: the first external adoption provides one.
- Specifying the practice: no numbered rules, no requirement keywords, no fixed vocabulary, until enough adoptions agree on what has stopped changing (D2).

## Requirements

- R1: A new adopter is pointed at two documents, the guide and the template, and each points the reader at the other: the guide by link, the template by URL in the instruction comment an author reads while filling it in.
- R2: Every section the template asks for is explained in the guide, with its reason.
- R3: No document in the repository directs a reader to a pattern page, and the only account of what lies beyond the practice is the guide's description of how a pattern is written and adopted.
- R4: No document in the repository states a rule by number or with a requirement keyword.
- R5: The guide and the template both say that a proposal is started before the work and is what the change is built from, by a person or an AI assistant.

## Decisions

- **D1: A small practice — the behavior-change trigger, the location and six sections; anything more is a pattern a team writes when it needs it.** A larger one — front matter, status, tiers, AI-draft markers — was rejected: each is needed only in situations some teams never meet, and a practice that assumes them pays their cost on every change from day one. The test for each part considered was "could a team use the practice for a year without this?"; only the six sections, the optional summary, the trigger and the location failed it. Human authorship, with a person approving each section an assistant drafted, was in that list at first and was taken out: the proposal is material an assistant may write as well as build from, and accountability for what it says is meant to sit in the process the change goes through, review included, not in who wrote it. A single prescribed process was rejected for the reason in `Problem`: adopted whole and abandoned, or adopted in part with the reasoning for the skipped parts lost. Revisit when an adoption adds the same pattern in its first week and the practice reads as broken without it; that pattern belongs in the practice, as `success-criteria` turned out to (D5).

- **D2: The practice is described, not specified.** A normative layout — a concept document, numbered principles, numbered rules with requirement keywords, and a rule table on every pattern page — was written first and then abandoned. It was being revised in place after a single adoption, which a specification cannot afford and a description can; and the numbering and identifier apparatus made the practice look settled when it is not. One guide now explains each part with its reason. Revisit when several adoptions agree on what has stopped changing; that part can then be stated as a rule.

- **D3: Documents only.** Shipping skills and a checker script was rejected: it would make the repository's shape and maintenance about tooling before the concept has been used by more than one team, and it would fix what tooling checks before adoptions agree on it (D2). Revisit after the first adopter builds either and reports what it needed.

- **D4: The patterns written ahead of their situations were withdrawn, not published as candidates.** Eighteen pattern pages were written first and placed in a catalog as unvalidated candidates; withholding them had been rejected on the reasoning that a team meeting one of their situations would otherwise have nothing to adopt. That was reversed for three reasons. The catalog behaved as a specification, with a shared section list, a front-matter schema, a status set and a web of dependencies between pages, so that every edit to the practice had to be checked against eighteen pages; that is the cost D2 was meant to remove, and it fell on this repository's every review. All but one of the pages had been written before anyone met their situation, which is the opposite of what a pattern is: an addition written when its situation has been met. And the one adoption that met a candidate's situation, drafting a proposal with an assistant, did not reach for the page, so the shelf did not do what publishing it assumed. The two pages that had met an adoption, `verification` and `human-ai-split`, went with the rest: what the adoption showed was that neither was needed from the first day, not that either was right. The pages remain in this repository's history at commit `31a47c7`, for anyone who meets one of their situations and wants a starting point. Revisit when an adoption meets a situation the practice does not cover and reports what it wrote; that page, written from use, is the first candidate.

- **D5: `success-criteria` was absorbed into the practice rather than kept as a pattern.** It began as a pattern page adding two sections, `Goals` and `Requirements`. Keeping it optional was rejected on the evidence of the first adoption, which needed both from day one: a practice whose first adopter has to add to it before writing anything is missing something. Both sections joined the practice, which is how it came to have six, and the page was deleted. This is the one absorption the record holds, and it is what D1's revisit clause points at. Revisit if adoptions leave either section empty often enough that filling it is ceremony; it would then go back to being a pattern.

## Risks

- Risk: without rules or tooling, consistency between proposals rests on the guide being read, and teams will drift. Accepted; the guide is short, and drift that matters will show up either as a situation a pattern can answer or as a rule worth stating once it has stopped changing.
- Risk: with no constraint on who writes a proposal, an assistant can write one and build from it without a person having decided anything in it. Accepted; accountability sits in the process the change goes through, review included, and a team that wants drafts marked or approved writes the pattern for it.
- Risk: with nothing published beyond the practice itself, teams that meet the same situation will answer it differently, and some will answer it worse than a pre-written page would have. Accepted; a page written from use is worth more than one written ahead of it, and a pull request is the way to bring it here.
- Risk: the practice has not been used on a real change in its described form; the one adoption so far exercised the earlier, specified form. Accepted; whether a description holds up as well as a rule set is what the next adoption tests.
