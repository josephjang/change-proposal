# Pattern: risk-signals

**Candidate.** Written before anyone met its situation; not validated. It may be validated by use, absorbed into the core, or dropped. See [the catalog](README.md).

Catches the changes whose cost of being wrong is high, before the code is written, with three questions instead of a rubric, so that everything else stays small.

**When.** The first change that someone wishes had been discussed before it was built.

**Goes with.** `design-first-review` (turns "a reviewer reads the draft" into a formal stage), `sizing-tiers` (the three signals become the ★ questions), `living-docs-bridge` (a signal triggers the living-docs section).

## What it adds

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

**One step.** When any answer is yes, one reviewer reads the draft, `Problem`, `Non-Goals`, `Decisions` so far, and the two sections above, before implementation code is written. A comment on the branch is enough.

**One line in the PR description**: which signals applied, or "none".

## Using it

- The author answers the three questions before implementation, every time. Signal-free changes cost one line in the PR.
- A yes brings the two sections and a reviewer before code. Ten minutes of a reviewer's time then is almost always repaid by not building the wrong thing.
- Two judgment calls the questions leave open, so that they do not become a rubric: a change that *reduces* exposure in a sensitive area may be treated as signal-free (the reviewer may raise it), and an internal interface whose consumers are all known and controlled by the same team may be treated as not a contract (the PR description says so).

## Knobs

Reviewers on a signal (default 1). Review turnaround (default one business day).

## Cost

Signal-free changes: one line in the PR. Changes with a signal: two sections and ten minutes of a reviewer's time before code.

## Removing it

Delete the questions and the two sections from the template. Proposals already carrying the sections remain valid. Without this pattern or `sizing-tiers`, the core's one question, "does behavior change?", is the whole of sizing, and which changes get a reader before the code is written is decided case by case.
