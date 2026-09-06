# Change Proposal: Initial release of the change-proposal practice

## Problem

Teams that build with AI assistants produce code faster than they record why. The judgment behind a change — what was rejected, what was knowingly accepted, what was actually verified — is lost in a chat transcript or written into a document away from the code that the next person or agent never reads. Existing document types (PRDs, design docs, ADRs) each cover part of this; none is sized for an ordinary change; and single prescribed processes get adopted whole and abandoned as ceremony, or adopted in part with the reasoning for the skipped parts lost.

## Goals
<!-- ai-draft -->

- A team can start recording the judgment behind its changes with one template and one short document to read, and nothing else.
- What the practice asks for can be understood in one sitting, with the reason next to each ask, so that a team adapting it can tell what to keep.
- The practice grows for a team without changing the core: a team adopts a pattern when its situation appears and drops it without touching what was written; changing the core itself is a separate change, recorded like any other (D6). Whatever a team might want beyond the core has at least a candidate written up far enough to try.

## Non-Goals
<!-- ai-draft -->

- Shipping tooling (lint, skills, a config format): the `lint-gate` and `agent-skills` pages say what it should do; implementations wait until the way repositories state which patterns they use has settled across a few adopters.
- Translating the practice's documents: English is the single source; non-English proposals in adopting repositories are the `multilingual-records` pattern.
- Recommending a set of patterns: the catalog gives starting points, not a verdict.
- Validating the candidate patterns: each waits on an adoption meeting its situation (D5).
- A worked example repository: the first external adoption provides one.
- Specifying the practice: no numbered rules, no requirement keywords, no fixed vocabulary, until enough adoptions agree on what has stopped changing (D2).

## Requirements
<!-- ai-draft -->

- R1: A new adopter is pointed at three documents, the guide, the template and the pattern catalog, and each points the reader at the other two: the guide and the catalog by link, the template by URL in the instruction comment an author reads while filling it in.
- R2: Every section the template asks for is explained in the guide, with its reason.
- R3: Every pattern named anywhere in the repository has a page, and every page names the situation that calls for it.
- R4: No document in the repository states a rule by number or with a requirement keyword.

## Decisions
<!-- ai-draft -->

- **D1: A small core — the behavior-change trigger, the location, human authorship and six sections; everything else is a pattern.** A larger core — front matter, status, tiers, AI-draft markers — was rejected: each is needed only in situations some teams never meet, and a core that assumes them pays their cost on every change from day one. The test for each part considered for the core was "could a team use the practice for a year without this?"; only the six sections, the optional summary, the trigger, the location and human authorship failed it. A single prescribed process was rejected for the reason in `Problem`: adopted whole and abandoned, or adopted in part with the reasoning for the skipped parts lost. Revisit when an adoption adds the same pattern in its first week and the practice reads as broken without it; that pattern is core material, as `success-criteria` turned out to be (D6).

- **D2: The practice is described, not specified.** A normative layout — a concept document, numbered principles, numbered rules with requirement keywords, and a rule table on every pattern page — was written first and then abandoned. It was being revised in place after a single adoption, which a specification cannot afford and a description can; and the numbering and identifier apparatus made the practice look settled when it is not. One guide now explains each part with its reason, and each pattern page says what it adds and when, in prose. Revisit when several adoptions agree on what has stopped changing; that part can then be stated as a rule.

- **D3: Which patterns a repository uses is stated in a sentence, not a configuration file.** A config file was rejected: it implies tooling that reads it, and the practice ships none. A sentence atop `docs/changes/README.md` serves people; tooling patterns may formalize it. Revisit when an implementation exists and prose proves ambiguous.

- **D4: Documents only.** Shipping skills and a checker script was rejected: it would make the repository's shape and maintenance about tooling before the concept has been used by more than one team. What the skills should do lives on the `agent-skills` page so an implementation can be checked against it. Revisit after the first adopter implements them.

- **D5: The patterns written so far are published as candidates, not as validated patterns.** Withholding them until validated was rejected: a team meeting one of their situations would have nothing to adopt, and validation needs exactly those adoptions. Presenting them as validated was rejected because it would be false: none has been through an adoption that settled it, and most were written before anyone met the situation they name. The first adoption has since met two of them: `verification` was split out of the core in response to it, and `human-ai-split` was rewritten on what it reported. Neither is thereby validated. The catalog says so on its first screen, and each candidate is validated, absorbed into the core, or dropped as adoptions meet it. Revisit per candidate, on evidence from adoptions.

- **D6: `success-criteria` was absorbed into the core rather than kept as a pattern.** It began as a pattern page adding two sections, `Goals` and `Requirements`. Keeping it optional was rejected on the evidence of the first adoption, which needed both from day one: a core whose first adopter must add a pattern before writing anything is not the core. Both sections joined the core, which is how it came to have six, the page was deleted, and the catalog went from nineteen entries to eighteen. This is the one absorption the record holds, and it is what D1's revisit clause points at. Revisit if adoptions leave either section empty often enough that filling it is ceremony; it would then go back to being a pattern.

## Verification
<!-- ai-draft -->

- Automated: a throwaway ripgrep/bash script over the tree (not shipped; non-goal) → 18 pattern pages, every one referenced from the catalog; 0 broken relative links; no rule identifier and no requirement keyword in any document; the template's sections are exactly `Summary`, `Problem`, `Goals`, `Non-Goals`, `Requirements`, `Decisions`, `Risks`, and the guide explains each.
- Manual: read-through of the guide, the catalog and each pattern page on the branch, checking that every page names its situation and what it adds.
- Not done, and why: the practice has not been used on a real change in its described form. The one adoption so far exercised the earlier, specified form; whether a description holds up as well as a rule set is what the next adoption tests.

## Risks
<!-- ai-draft -->

- Risk: without rules or tooling, consistency between proposals rests on the guide being read, and teams will drift. Accepted; the guide is short, and drift that matters will show up either as a situation a pattern can answer or as a rule worth stating once it has stopped changing.
- Risk: a catalog this size may read as a set of validated patterns, or as a menu to work through. Accepted; the catalog says on its first screen that none has been validated, and the question-first table keeps a reader from working through them in order.
