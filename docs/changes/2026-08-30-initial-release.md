# Change Proposal: Initial release of the change-proposal practice

## Problem

Teams that build with AI assistants produce code faster than they record why. The judgment behind a change — what was rejected, what was knowingly accepted, what was actually verified — is lost in a chat transcript or written into a document away from the code that the next person or agent never reads. Existing document types (PRDs, design docs, ADRs) each cover part of this; none is sized for an ordinary change; and single prescribed processes get adopted whole and abandoned as ceremony, or adopted in part with the reasoning for the skipped parts lost.

## Goals
<!-- ai-draft -->

- A team can start recording the judgment behind its changes with one template and one short document to read, and nothing else.
- What the practice asks for can be understood in one sitting, with the reason next to each ask, so that a team adapting it can tell what to keep.
- Whatever a team might want later has a thought-through answer it can pick up on its own, without the practice assuming it.

## Non-Goals
<!-- ai-draft -->

- Shipping tooling (lint, skills, a config format): the `lint-gate` and `agent-skills` pages say what it should do; implementations wait until the way repositories state which patterns they use has settled across a few adopters.
- Translating the practice's documents: English is the single source; non-English proposals in adopting repositories are the `multilingual-records` pattern.
- Recommending a set of patterns: the catalog gives starting points, not a verdict.
- A worked example repository: the first external adoption provides one.
- Specifying the practice: no numbered rules, no requirement keywords, no fixed vocabulary, until enough adoptions agree on what has stopped changing (D2).

## Requirements
<!-- ai-draft -->

- R1: A new adopter is pointed at three documents, the guide, the template and the pattern catalog, and each links to the other two.
- R2: Every section the template asks for is explained in the guide, with its reason.
- R3: Every pattern named anywhere in the repository has a page, and every page names the situation that calls for it.
- R4: No document in the repository states a rule by number or with a requirement keyword.

## Decisions
<!-- ai-draft -->

- **D1: Six sections and nothing else required; everything further is optional.** A larger base — front matter, status, tiers, AI-draft markers — was rejected: each is needed only in situations some teams never meet, and a base that assumes them pays their cost on every change from day one. The test for every candidate was "could a team use the practice for a year without this?"; only the six sections, the optional summary, the trigger, the location and human authorship failed it. Revisit if adopters consistently add the same pattern in their first week.

- **D2: The practice is described, not specified.** A normative layout — a concept document, numbered principles, numbered rules with requirement keywords, and a rule table on every pattern page — was written first and then abandoned. It was being revised in place after a single adoption, which a specification cannot afford and a description can; and the numbering and identifier apparatus made the practice look settled when it is not. One guide now explains each part with its reason, and each pattern page says what it adds and when, in prose. Revisit when several adoptions agree on what has stopped changing; that part can then be stated as a rule.

- **D3: Which patterns a repository uses is stated in a sentence, not a configuration file.** A config file was rejected: it implies tooling that reads it, and the practice ships none. A sentence atop `docs/changes/README.md` serves people; tooling patterns may formalize it. Revisit when an implementation exists and prose proves ambiguous.

- **D4: Documents only.** Shipping skills and a checker script was rejected: it would make the repository's shape and maintenance about tooling before the concept has been used by more than one team. What the skills should do lives on the `agent-skills` page so an implementation can be checked against it. Revisit after the first adopter implements them.

## Verification
<!-- ai-draft -->

- Automated: a throwaway ripgrep/bash script over the tree (not shipped; non-goal) → 18 pattern pages, every one referenced from the catalog; 0 broken relative links; no rule identifier and no requirement keyword in any document; the template's sections are exactly `Summary`, `Problem`, `Goals`, `Non-Goals`, `Requirements`, `Decisions`, `Risks`, and the guide explains each.
- Manual: read-through of the guide, the catalog and each pattern page on the branch, checking that every page names its situation and what it adds.
- Not done, and why: the practice has not been used on a real change in its described form. The one adoption so far exercised the earlier, specified form; whether a description holds up as well as a rule set is what the next adoption tests.

## Risks
<!-- ai-draft -->

- Risk: without rules or tooling, consistency between proposals rests on the guide being read, and teams will drift. Accepted; the guide is short, and drift that matters will show up either as a situation a pattern can answer or as a rule worth stating once it has stopped changing.
- Risk: eighteen patterns may read as a menu rather than a shelf. Accepted; the question-first catalog and the starting points (four patterns suffice) push the other way.
