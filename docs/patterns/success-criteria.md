# Pattern: success-criteria

- **Requires**: core
- **Combines with**: `agent-context` (requirements are an agent's stopping condition), `outcome-review` (metrics declared here are compared with actuals), `initiative-umbrella` (a brief always has them)
- **Conflicts with**: —

## Intent

Give the proposal a definition of "done" that can be judged true or false, and make goals explicit alongside the non-goals the core already requires.

## Signal

"Is it done?" is disputed at review time, or someone other than the author — a colleague, an agent — implements from the proposal and needs to know when to stop.

## Adds

**Two sections.** `Goals`, placed directly before `Non-Goals`:

```
## Goals
- (end states — "X is possible", not "build X")
```

`Requirements`, placed directly after `Non-Goals`:

```
## Requirements
- R1: (a statement judgeable true or false)
- R2:
- (optional) Metric: (name) baseline (value) → target (value), (how measured)
```

The requirements are the stopping condition: when every one is true, the work is done and anything further is a new change.

## Rules

| ID | Rule | Principle |
|---|---|---|
| **SC1** | `Goals` MUST contain at least one goal stated as an end state. | P2 |
| **SC2** | `Requirements` MUST consist of two to four statements, each judgeable true or false. | P2 |
| **SC3** | A metric, when declared, MUST carry a baseline, a target and a measurement method. | P2 |

## Cost

Two to four lines, written at the moment the problem is clearest. The hard part is refusing vague criteria; that is the point.

## Remove

Drop `Goals` and `Requirements` from the template (`Non-Goals` stays; it is core). Existing proposals stay as they are.
