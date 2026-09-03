# Pattern: sizing-tiers

- **Requires**: core, `proposal-metadata` (for the `tier` field)
- **Combines with**: `risk-signals` (its three questions are the ★ rows of the rubric), `design-first-review` (tier ≥ T2 triggers the stage), `initiative-umbrella` (T3 is an initiative), `before-after` and `success-criteria` (required at T2+), `lint-gate`
- **Conflicts with**: —

## Intent

Replace "does behavior change?" plus three risk questions with an explicit, lint-able tier, when a team needs more resolution than "ordinary or risky".

## Signal

Recurring after-the-fact arguments — "this should have had more review", "this did not need all that" — that the three risk signals do not settle. Typically past a few dozen proposals or past one team.

## Adds

**A front-matter field**: `tier: T0 | T1 | T2 | T3`.

**A rubric** — eight yes/no questions; a ★ answered yes puts the change at T2 by itself:

| | Question |
|---|---|
| A | Does user-visible behavior change? (restoring intended behavior does not count) |
| B ★ | Does a contract others depend on change? |
| C ★ | Is it hard to reverse? |
| D ★ | Does it touch auth, permissions, personal data, payments or a regulated area? |
| E | Is the problem itself uncertain — we do not know what to build? |
| F | Do two or more teams or services have to cooperate? |
| G | Will it exceed one person-week or three pull requests? |
| H | Does it need a staged rollout? |

| Tier | Condition | Document |
|---|---|---|
| **T0** | All no, and no behavior change | PR description only |
| **T1** | No ★, 0–1 yes | Core proposal |
| **T2** | Any ★, or 2–3 yes | Core + `Summary` + `Change` + `Requirements` + `Rollout & rollback` + `Cross-cutting concerns` (+ `Living docs` if that pattern is on) |
| **T3** | 4+ yes, or E and F both yes | `initiative-umbrella` |

**A `Summary` section** for T2 and above, directly under the title: three to five sentences — what changes, why, what does not change.

**Per-tier word caps** (defaults): T1 500, T2 1,500, T3 brief 2,000 / design 4,000.

**An edge-case table** kept in the repository's `docs/changes/README.md`, grown as cases are met. Seed entries: a large mechanical refactor with identical behavior is T0; a one-line permission change is T2; an internal interface whose consumers are all in-team is T1; masking a leaked field is T1 (reviewer may raise).

## Rules

| ID | Rule | Principle |
|---|---|---|
| **ST1** | Front matter MUST carry `tier`, determined by the rubric. T0 means no proposal. | P1 |
| **ST2** | The tier MUST be proposed by the author with one line of reasoning in the PR and confirmed by a reviewer. When unsure, the higher tier MUST be chosen; the reviewer MAY lower it. | P1 |
| **ST3** | Raising a tier MUST be done by adding sections and changing `tier`; the file MUST NOT be moved. | P7 |
| **ST4** | T2 and above MUST include `Summary`, `Change`, `Requirements`, `Rollout & rollback` and `Cross-cutting concerns`. | P1 |
| **ST5** | Word caps per tier apply as recorded in the repository's composition. | P9 |

## Parameters

Word caps per tier. The edge-case table.

## Cost

One more explicit decision per change. Watch for tier inflation or deflation; the share of tiers changed in review should stay under about 15 %.

## Remove

Delete `tier` from the template and return to `risk-signals` alone. Existing `tier` values are harmless.
