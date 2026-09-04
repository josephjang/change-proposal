# Pattern: sizing-tiers

Replaces "does behavior change?" plus three risk questions with an explicit, lint-able tier, for a team that needs more resolution than "ordinary or risky".

**When.** Recurring after-the-fact arguments, "this should have had more review", "this did not need all that", that the three risk signals do not settle. Typically past a few dozen proposals or past one team.

**Needs.** `proposal-metadata` (for the `tier` field). Goes with `risk-signals` (its three questions are the ★ rows of the rubric), `design-first-review` (tier T2 and above triggers the stage), `initiative-umbrella` (T3 is an initiative), `before-after` (its `Change` is expected at T2 and above), `lint-gate`.

## What it adds

**A front-matter field**: `tier: T0 | T1 | T2 | T3`.

**A rubric**: eight yes/no questions; a ★ answered yes puts the change at T2 by itself.

| | Question |
|---|---|
| A | Does user-visible behavior change? (restoring intended behavior does not count) |
| B ★ | Does a contract others depend on change? |
| C ★ | Is it hard to reverse? |
| D ★ | Does it touch auth, permissions, personal data, payments or a regulated area? |
| E | Is the problem itself uncertain: we do not know what to build? |
| F | Do two or more teams or services have to cooperate? |
| G | Will it exceed one person-week or three pull requests? |
| H | Does it need a staged rollout? |

| Tier | Condition | Document |
|---|---|---|
| **T0** | All no, and no behavior change | PR description only |
| **T1** | No ★, 0–1 yes | The six sections |
| **T2** | Any ★, or 2–3 yes | The six sections + `Summary` + `Change` + `Rollout & rollback` + `Cross-cutting concerns` (+ `Living docs` if that pattern is on) |
| **T3** | 4+ yes, or E and F both yes | `initiative-umbrella` |

At T2 and above the guide's optional `Summary` becomes expected.

**Per-tier word caps** (defaults): T1 500, T2 1,500, T3 brief 2,000 / design 4,000.

**An edge-case table** kept in the repository's `docs/changes/README.md`, grown as cases are met. Seed entries: a large mechanical refactor with identical behavior is T0; a one-line permission change is T2; an internal interface whose consumers are all in-team is T1; masking a leaked field is T1 (reviewer may raise).

## Using it

- The author proposes the tier with one line of reasoning in the PR; a reviewer confirms. When unsure, pick the higher tier; the reviewer can lower it.
- Raising a tier means adding sections and changing `tier`. The file does not move.
- Word caps apply as recorded with the pattern list.
- Watch for tier inflation or deflation. If more than about 15 % of tiers change in review, the rubric or the edge-case table needs work.

## Knobs

Word caps per tier. The edge-case table.

## Cost

One more explicit decision per change.

## Removing it

Delete `tier` from the template and return to `risk-signals` alone. Existing `tier` values are harmless.
