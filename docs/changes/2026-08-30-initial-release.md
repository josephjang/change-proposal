# Initial release of the change-proposal practice

## Problem

Teams that build with AI assistants produce code faster than they record why. The judgment behind a change — what was rejected, what was knowingly accepted, what was actually verified — is lost in a chat transcript or written into a document away from the code that the next person or agent never reads. Existing document types (PRDs, design docs, ADRs) each cover part of this; none is sized for an ordinary change; and single prescribed processes get adopted whole and abandoned as ceremony, or adopted in part with the reasoning for the skipped parts lost.

## Non-Goals

- Shipping tooling (lint, skills, a config format): the `lint-gate` and `agent-skills` cards specify it; implementations wait until the composition statement has settled across a few adopters.
- Translating the practice's documents: English is the single source; non-English proposals in adopting repositories are the `multilingual-records` pattern.
- Recommending a composition: the catalog gives examples, not a verdict.
- A worked example repository: the first external adoption provides one.

## Decisions

- **D1: A four-section core, everything else a pattern.** A larger core — front matter, status, tiers, AI-draft markers — was rejected: each is needed only in situations some teams never meet, and a core that assumes them pays their cost on every change from day one. The test for every candidate was "could a team use the practice for a year without this?"; only the four sections, the optional summary, the trigger, the location, human authorship and the one-page rule failed it. Revisit if adopters consistently add the same pattern in their first week.

- **D2: Patterns carry their own rules.** One rules document tagged by pattern was rejected: it made the core look larger than it is and made readers of one pattern navigate sixty rules. Each card is self-contained; `docs/rules.md` holds eight core rules and the questions the core does not answer. Revisit if rules get duplicated across cards.

- **D3: Composition is declared in prose, not configuration.** A config file was rejected for the core: it implies tooling that reads it, and the core ships none. A sentence atop `docs/changes/README.md` serves people; tooling patterns may formalize it. Revisit when an implementation exists and prose proves ambiguous.

- **D4: Documents only.** Shipping skills and a checker script was rejected: it would make the repository's shape and maintenance about tooling before the concept has been used by anyone. Skill specifications live in the `agent-skills` card so an implementation can be verified against them. Revisit after the first adopter implements them.

## Verification

- Checked: every pattern name used in the concept, rules and catalog has a card (19); every rule id cited in a card is defined there; every relative link resolves; the core template has exactly the core sections. Done with a throwaway script over the tree, not shipped (non-goal).
- Not checked, and why: the practice has not been used on a real change by anyone but its authors. The first external adoption is the test; its findings arrive as proposals.

## Risks

- Risk: without tooling, every rule is review-enforced; stretched reviewers will let markers and stale sections through. Accepted; the `lint-gate` card specifies the fix.
- Risk: nineteen patterns may read as a menu rather than a shelf. Accepted; P10 and the example compositions (four patterns suffice) push the other way.
