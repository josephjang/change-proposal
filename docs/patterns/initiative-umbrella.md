# Pattern: initiative-umbrella

- **Requires**: core, `proposal-metadata` (for `parent` and status), `design-first-review` (briefs and designs are reviewed before investment), `success-criteria` (a brief declares metrics)
- **Combines with**: `sizing-tiers` (an initiative is T3), `outcome-review` (initiatives always get one), `living-docs-bridge`, `decision-promotion`
- **Conflicts with**: —

## Intent

Handle work too large for one proposal — weeks, several people, several pull requests — without inventing a separate planning-document culture: an initiative is a brief, a design and a set of ordinary proposals that point at them.

## Signal

A month-plus, multi-team initiative starts, or the problem itself is uncertain and cross-team at once. Before that the pattern is pure overhead.

## Adds

**A directory per initiative** under `docs/changes/`, sharing one id:

```
docs/changes/YYYY-MM-DD-<slug>/
  brief.md
  design.md
  outcome.md        (with outcome-review)
```

**The brief** (≈2,000 words), reviewed to `accepted` by the product owner and the technical lead. Sections: `Summary`, `Problem`, `Goals` (with an *appetite* — how much time or effort the problem is worth), `Non-Goals`, `Requirements` (metrics with baseline, target, method, when measured), `Decisions` (scope, audience, sequencing), `Milestones` (stage, audience, condition to advance, rollback trigger), `Risks & deferred`, `Open questions`.

**The design** (≈4,000 words), reviewed to `accepted` technically. Sections: `Summary`, `Current structure` (how it works today and the constraints), `Goals`, `Non-Goals` (technical), `Design` (structure with one diagram; contracts that have no code yet; data flow and state), `Decisions` (a table: chosen, rejected, reason, revisit when), `Cross-cutting concerns`, `Rollout & rollback`, `Verification` (strategy at accepted; end-to-end results at implemented; the list of child proposals), `Risks & deferred`, `Living docs`, `Open questions`.

**A front-matter field** on child proposals: `parent: CP-YYYY-MM-DD-<slug>`. The design keeps the list of children with their status.

## Rules

| ID | Rule | Principle |
|---|---|---|
| **IU1** | An initiative MUST be a directory containing `brief.md` and `design.md`, sharing one id. | P7 |
| **IU2** | Every child proposal MUST set `parent`, and `design.md` MUST list the children with their status. | P7 |
| **IU3** | The brief MUST state an appetite and metrics with baseline, target and measurement method. | P2 |
| **IU4** | The design MUST hold structure, contracts and decisions only; implementation detail belongs in child proposals and work breakdown in the tracker. | P2 |

## Parameters

Brief reviewers (default: product owner + technical lead). Word caps (defaults above).

## Cost

Two reviewed documents before investment and the discipline of decomposition. For work of this size, the alternative costs more.

## Remove

Stop creating initiative directories; existing ones remain valid records.
