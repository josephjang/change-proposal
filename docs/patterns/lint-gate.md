# Pattern: lint-gate

- **Requires**: core, `proposal-metadata` (most checks read front matter)
- **Combines with**: every pattern with a mechanical rule (`human-ai-split`, `evidence-verification`, `supersession`, `sizing-tiers`, `design-first-review`, `living-docs-bridge`, `decision-promotion`, `initiative-umbrella`, `outcome-review`, `agent-context`, `multilingual-records`)
- **Conflicts with**: —

## Intent

Move the mechanical rules — file placement, front matter, markers, caps, immutability, required sections — out of reviewers' heads and into CI, so review time is spent on judgment.

## Signal

A proposal merged with `<!-- ai-draft -->` markers still in it, a behavior change merged without a proposal, or a merged proposal edited in place. One occurrence is enough.

## Adds

**A lint specification.** This pattern specifies the checks; an adopter implements them (a few hundred lines in any scripting language, no dependencies beyond git) and records the implementation in a proposal. Each check is active only when the pattern that introduces its rule is adopted.

| Check | Rule | Active when |
|---|---|---|
| File at `docs/changes/YYYY-MM-DD-<slug>.md` | C2 | always |
| Section labels from the table; core sections present | C3 | always |
| `Non-goals` non-empty; `Decisions` entries have a rejected alternative and a reason; `Verification` has a "not checked" statement | C6, C7, C8 | always (heuristic; warning only) |
| Word cap | C8 | always (warning) |
| Front matter present, required fields, allowed `status` values, `id` agrees with the file name | PM1, PM2, PM4 | `proposal-metadata` |
| No `<!-- ai-draft` marker in a proposal at `implemented` / `accepted` | HA2 | `human-ai-split` |
| "Not done, and why" entry present | EV2 | `evidence-verification` |
| Body of `implemented` / `superseded` proposals unchanged against a base ref; only `status` and `superseded_by` may change | SU1 | `supersession` |
| `tier` valid; tier-specific sections and caps | ST1, ST4, ST5 | `sizing-tiers` |
| `Open questions` empty at `implemented` | DF3 | `design-first-review` |
| `Living docs` present where required | LD1 | `living-docs-bridge` |
| Promoted decisions and records reference each other | DP2 | `decision-promotion` |
| Initiative directories complete; `parent` values resolve | IU1, IU2 | `initiative-umbrella` |
| Outcome review exists by `review_on` plus grace | OR1 | `outcome-review` |
| `touches` values in the declared vocabulary | AC4 | `agent-context` (with a vocabulary) |
| Headings resolve to a known label in either form; front matter English | ML2, ML3 | `multilingual-records` |

**An enforcement level per check** — `warn` or `block` — recorded in `docs/changes/README.md`. Start at `warn`; move the checks that matter to `block` after a few weeks of clean runs.

**A boundary**: the lint checks shape, never content. It cannot tell whether a rejection reason is real or whether a verification line was run; that stays with the reviewer, and freeing the reviewer for exactly that is the point.

## Rules

| ID | Rule | Principle |
|---|---|---|
| **LG1** | CI MUST run the lint over `docs/changes/` on every pull request. | P9 |
| **LG2** | The enforcement level MUST be recorded in the composition and MAY differ per check. | P10 |
| **LG3** | The lint MUST implement at least the checks marked "always" and the checks of every adopted pattern. | P9 |

## Cost

A CI step and occasional false positives when the composition statement and the lint drift.

## Remove

Remove the CI step. Rules revert to review-enforced.
