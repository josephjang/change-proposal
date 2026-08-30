# Pattern: design-first-review

- **Requires**: core, `proposal-metadata` (for the `accepted` status), and one of `risk-signals` or `sizing-tiers` (to know which proposals get the stage)
- **Combines with**: `spike-then-spec` (together they say when a prototype may reach main), `initiative-umbrella` (briefs and designs always pass through this stage)
- **Conflicts with**: —

## Intent

Turn "a reviewer reads the draft before code" into a named stage (`accepted`) reached through a docs-only pull request, for the changes where a comment on a branch is not enough to stop a wrong design.

## Signal

Risky changes keep arriving as finished code and reviewers say they cannot push back on the design because the work is already done. Or the `risk-signals` pre-code read is being skipped because nothing enforces it.

## Adds

**A status value**: `accepted`, between `draft` and `implemented`.

**A two-stage flow** for proposals with a risk signal (or tier ≥ T2):

1. *Design PR* — the proposal with every section except `Verification`, `Risks & deferred` and `Living docs`, plus `Open questions`. Docs only. Reviewed within the agreed turnaround. Merged → `accepted`.
2. *Implementation PR(s)* — each appends itself to `prs`; the last fills the remaining sections, empties `Open questions` (answers move into `Decisions`), and sets `implemented`.

**One section** for the design stage:

```
## Open questions
| # | Question | Owner | Due |
|---|---|---|---|
```

**A prototype rule**: prototype code does not reach the main branch before `accepted`, unless behind a flag that is off by default.

**A short-cut**: a proposal whose design is obviously short (one signal, no alternatives) may merge both PRs together if the reviewer approves the document before the code.

## Rules

| ID | Rule | Principle |
|---|---|---|
| **DF1** | A proposal with a risk signal (or tier ≥ T2) MUST reach `accepted` through a docs-only pull request before implementation code is merged. | P1, P3 |
| **DF2** | Prototype code MUST NOT reach the main branch before `accepted`, unless behind a flag that is off by default. | P1 |
| **DF3** | `Open questions` MUST be empty at `implemented`; answers MUST be moved into `Decisions` and the section deleted. | P2 |
| **DF4** | A proposal with one signal and no alternatives MAY merge the design and implementation PRs together if the reviewer approves the document before the code. | P9 |

## Parameters

Design reviewers (default 1; product and technical for initiatives). Design review turnaround (default two business days).

## Cost

One more pull request per risky change and a review turnaround the team has to honor. Teams with a review-latency problem will find this exposes it.

## Remove

Drop `accepted` and `Open questions`; fall back to the `risk-signals` comment-on-branch read. Existing `accepted` proposals stay as they are.
