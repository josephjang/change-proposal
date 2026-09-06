# Pattern: initiative-umbrella

**Candidate.** Written before anyone met its situation; not validated. It may be validated by use, absorbed into the core, or dropped. See [the catalog](README.md).

Handles work too large for one proposal, weeks, several people, several pull requests, without inventing a separate planning-document culture: an initiative is a brief, a design and a set of ordinary proposals that point at them.

**When.** A month-plus, multi-team initiative starts, or the problem itself is uncertain and cross-team at once. Before that the pattern is pure overhead.

**Needs.** `proposal-metadata` (for `parent` and status) and `design-first-review` (briefs and designs are reviewed before investment). Goes with `sizing-tiers` (an initiative is T3), `outcome-review` (initiatives always get one), `living-docs-bridge`, `decision-promotion`.

## What it adds

**A directory per initiative** under `docs/changes/`, sharing one id:

```
docs/changes/YYYY-MM-DD-<slug>/
  brief.md
  design.md
  outcome.md        (with outcome-review)
```

**The brief** (about 2,000 words), reviewed to `accepted` by the product owner and the technical lead. Sections: `Summary`, `Problem`, `Goals` (with an *appetite*: how much time or effort the problem is worth), `Non-Goals`, `Requirements` (metrics with baseline, target, method, when measured), `Decisions` (scope, audience, sequencing), `Milestones` (stage, audience, condition to advance, rollback trigger), `Risks`, `Open questions`.

**The design** (about 4,000 words), reviewed to `accepted` technically. Sections: `Summary`, `Current structure` (how it works today and the constraints), `Goals`, `Non-Goals` (technical), `Design` (structure with one diagram; contracts that have no code yet; data flow and state), `Decisions` (a table: chosen, rejected, reason, revisit when), `Cross-cutting concerns`, `Rollout & rollback`, `Verification` (strategy at accepted; end-to-end results at implemented; the list of child proposals), `Risks`, `Living docs`, `Open questions`.

**A front-matter field** on child proposals: `parent: CP-YYYY-MM-DD-<slug>`. The design keeps the list of children with their status.

## Using it

- Every child proposal sets `parent`, and the design lists the children with their status, so the initiative can be read from either end.
- The brief states an appetite and metrics with baseline, target and measurement method; without those, the initiative has no way to say it is done or that it worked.
- The design holds structure, contracts and decisions only. Implementation detail belongs in child proposals, work breakdown in the tracker.

## Knobs

Brief reviewers (default: product owner + technical lead). Word caps (defaults above).

## Cost

Two reviewed documents before investment and the discipline of decomposition. For work of this size, the alternative costs more.

## Removing it

Stop creating initiative directories; existing ones remain valid records.
