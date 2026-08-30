# Pattern: risk-signals

- **Requires**: core
- **Combines with**: `design-first-review` (turns "a reviewer reads the draft" into a formal stage), `sizing-tiers` (the three signals become the ★ questions), `living-docs-bridge` (a signal triggers the living-docs requirement)
- **Conflicts with**: —

## Intent

Catch the changes whose cost of being wrong is high — before the code is written — with three questions instead of a rubric, so that everything else stays one page.

## Signal

The first change that someone wishes had been discussed before it was built. Most teams meet this within weeks; adopting it with the core is reasonable.

## Adds

**Three questions**, answered by the author before implementation:

| Signal | Question | Typical "yes" |
|---|---|---|
| **Contract** | Does something that other code, another team or an external party depends on change? | API, database schema, event payload, config file format, CLI flags, webhook format. An *added* field counts if a consumer parses strictly. |
| **Irreversible** | Is it hard to undo? | Migration or backfill, data deletion, external announcement or email, payments, index rebuilds that take hours. "Flag off restores everything" is a no. |
| **Sensitive** | Does it touch auth, permissions, personal data, payments or a regulated area? | Login, sessions, permission checks, PII storage / exposure / logging, payment flows, audit logs, consent. |

**Two sections**, added when any answer is yes:

```
## Rollout & rollback
- Contract that changes: (until code exists, this is the source of truth; replace with a path after)
- Order: (e.g. migration → server → client; behavior in the intermediate state)
- Flag / stages:
- Rollback: (is flag-off enough? what about data?)
- Check right after deploy:

## Cross-cutting concerns
- Security / personal data:
- Compatibility:
- Observability (logs · metrics · alerts):
- Failure behavior (retries · idempotency · dependency outage):
  (write "n/a — reason" where something does not apply; that is the evidence it was considered)
```

**One step**: when any answer is yes, one reviewer reads the draft — Problem, Non-goals, Decisions so far, and the two sections above — before implementation code is written. A comment on the branch is enough.

**One line in the PR description**: which signals applied, or "none".

## Rules

| ID | Rule | Principle |
|---|---|---|
| **RS1** | Before implementation, the author MUST answer the three questions. | P1 |
| **RS2** | If any answer is yes, the proposal MUST include `Rollout & rollback` and `Cross-cutting concerns`, and one reviewer MUST read the draft before implementation code is written. | P1 |
| **RS3** | The PR description MUST state which signals applied, or "none". | P1 |
| **RS4** | A change that reduces exposure in a sensitive area MAY be treated as signal-free; the reviewer MAY raise it. | P1 |
| **RS5** | An internal interface whose consumers are all known and controlled by the same team MAY be treated as not a contract; the PR description MUST say so. | P1 |

## Parameters

Reviewers on a signal (default 1). Review turnaround (default one business day).

## Cost

Signal-free changes: one line in the PR. Changes with a signal: two sections and ten minutes of a reviewer's time before code — almost always repaid by not building the wrong thing.

## Remove

Delete the questions and the two sections from the template. Proposals already carrying the sections remain valid. Without this pattern or `sizing-tiers` the practice has no sizing beyond "does behavior change?", which is a legitimate choice only for small, low-risk codebases.
