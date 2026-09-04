# Rules

The normative part of the core. Twelve rules; nothing else is required of a team that has adopted no pattern. Each pattern carries its own rules in its card (`docs/patterns/<name>.md`), and a repository is bound by the core rules plus the rules of the patterns it lists in `docs/changes/README.md`.

Keywords follow RFC 2119: **MUST** / **MUST NOT** are requirements; **SHOULD** is a strong default that a proposal may override with a stated reason; **MAY** is optional.

When a rule and a principle conflict in a concrete case, the principle wins and the rule needs a proposal.

---

## Core rules

| ID | Rule |
|---|---|
| **C1** | A change that alters observable behavior MUST have a proposal. A change that does not — refactor with identical behavior, typo, dependency patch, tests only — MUST NOT have one; its pull-request description MUST say there is no behavior change and how that was checked. |
| **C2** | The proposal MUST be committed in the same pull request as the change. By default it lives at `docs/changes/YYYY-MM-DD-<slug>.md` — or, as a set of documents, at `docs/changes/YYYY-MM-DD-<slug>/`; a repository with its own document location or naming convention MAY use that instead. |
| **C3** | The proposal MUST consist of a title and sections with exactly these labels, in this order: `Problem`, `Goals`, `Non-Goals`, `Requirements`, `Decisions`, `Risks`. A section with nothing to say MUST be deleted. Sections added by adopted patterns use the labels those patterns define. |
| **C4** | A person MUST write the proposal or explicitly approve each of its sections before merge. Material may come from anywhere; the text of each section is a person's judgment. |
| **C5** | The proposal MUST NOT reproduce content whose source of truth is the code, the tests or the tracker — schemas, signatures, payloads, file lists, task breakdowns. It MUST reference them instead. |
| **C6** | `Non-Goals` MUST contain at least one item, each with its reason. |
| **C7** | `Decisions` MUST contain only decisions that had alternatives. Each entry MUST name what was chosen, what was rejected, and a reason of the kind that would change if the facts changed. It SHOULD name the condition under which the decision would be revisited. An entry whose premise turns out to be false was never a decision: it MUST be deleted, and the deletion MUST prompt a check of what leaves the code with it. |
| **C8** | `Goals` MUST contain at least one goal stated as an end state. |
| **C9** | `Requirements` MUST contain at least one statement, each judgeable true or false. A metric, when declared, MUST carry a baseline, a target and a measurement method. |
| **C10** | The title SHOULD carry the `Change Proposal: ` prefix; a repository that marks documents its own way — an identifier scheme, a date — MAY use that marker instead. |
| **C11** | A `Summary` MAY precede `Problem`: three to five sentences directly under the title — what changes, why, what does not change. |
| **C12** | `Decisions` MAY be split into `Product Decisions` followed by `Technical Decisions` when both kinds are present — a decision is product if reversing it changes what the team experiences or what a standard means, technical if only the code changes; C7 applies to each. |

---

## What the core rules do not say

The following are common questions whose answers are patterns, not core rules. A team that has not adopted the pattern has no rule on the matter and decides case by case.

| Question | Pattern |
|---|---|
| Does this change need review before code is written? | `risk-signals`, `design-first-review` |
| Is there a tier or size label? | `sizing-tiers` |
| May a merged proposal be edited? How is one reversed? | `supersession` |
| Is there front matter — owner, status, links, tags? | `proposal-metadata` |
| Must the proposal say what was verified? | `verification` |
| Must it describe what changed? | `before-after` |
| May an assistant draft parts of it, and how is that marked? | `human-ai-split` |
| Must Verification be commands and outputs? | `evidence-verification` |
| Must it list the documents it made stale? | `living-docs-bridge` |
| Where do standards go? | `decision-promotion` |
| How is multi-week work organized? | `initiative-umbrella` |
| Is the outcome ever revisited? | `outcome-review` |
| Do agents read proposals? Are there skills? | `agent-context`, `agent-skills` |
| Does CI check anything? | `lint-gate` |
| May proposals be written in another language? | `multilingual-records` |
