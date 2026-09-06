# Pattern: lint-gate

**Candidate.** Written before anyone met its situation; not validated. It may be validated by use, absorbed into the core, or dropped. See [the catalog](README.md).

Moves the mechanical checks, file placement, front matter, markers, caps, immutability, required sections, out of reviewers' heads and into CI, so review time is spent on judgment.

**When.** A proposal merged with `<!-- ai-draft -->` markers still in it, a behavior change merged without a proposal, or a merged proposal edited in place. One occurrence is enough.

**Needs.** `proposal-metadata` (most checks read front matter). Goes with every pattern that has a mechanical rule.

## What it adds

**A list of checks.** This pattern says what to check; an adopter implements it (a few hundred lines in any scripting language, no dependencies beyond git) and records the implementation in a proposal. Each check is active only when the pattern that calls for it is in use.

| Check | Active when |
|---|---|
| The file is at `docs/changes/YYYY-MM-DD-<slug>.md`, or at the repository's own location | always |
| Section names come from the shared list; the guide's sections are present | always |
| `Goals` and `Non-Goals` non-empty; each `Decisions` entry (split or not) has a rejected alternative and a reason; `Requirements` has at least one statement | always (heuristic; warning only) |
| Front matter present with the required fields; `status` is an allowed value; `id` agrees with the file name | `proposal-metadata` |
| No `<!-- ai-draft` marker in a proposal at `implemented` / `accepted` | `human-ai-split` |
| `Verification` present with a "not checked" line | `verification` (heuristic; warning only) |
| "Not done, and why" entry present | `evidence-verification` |
| Body of `implemented` / `superseded` proposals unchanged against a base ref; only `status` and `superseded_by` may change | `supersession` |
| `tier` valid; tier-specific sections and word caps | `sizing-tiers` |
| `Open questions` empty at `implemented` | `design-first-review` |
| `Living docs` present where required | `living-docs-bridge` |
| Promoted decisions and records reference each other | `decision-promotion` |
| Initiative directories complete; `parent` values resolve | `initiative-umbrella` |
| Outcome review exists by `review_on` plus grace | `outcome-review` |
| `touches` values in the declared vocabulary | `agent-context` (with a vocabulary) |
| Headings resolve to a known section name in either form; front matter English | `multilingual-records` |

**An enforcement level per check**, `warn` or `block`, recorded next to the pattern list in `docs/changes/README.md`. Start at `warn`; move the checks that matter to `block` after a few weeks of clean runs.

**A boundary.** The lint checks shape, never content. It cannot tell whether a rejection reason is real or whether a verification line was run; that stays with the reviewer, and freeing the reviewer for exactly that is the point.

## Using it

- CI runs the lint over `docs/changes/` on every pull request.
- The lint implements at least the always-on checks and the checks of every pattern in use; a check for a pattern not in use is noise.
- The enforcement level is recorded with the pattern list and may differ per check.

## Cost

A CI step and occasional false positives when the pattern list and the lint drift.

## Removing it

Remove the CI step. Checks revert to reviewers.
