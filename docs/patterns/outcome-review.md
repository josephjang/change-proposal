# Pattern: outcome-review

- **Requires**: core, `success-criteria` (there must be a declared metric to compare against)
- **Combines with**: `initiative-umbrella` (always on for initiatives), `supersession` (an outcome is immutable once written), `proposal-metadata` (a `review_on` date)
- **Conflicts with**: —

## Intent

Close the loop on the metrics a proposal declared, and record where the prediction was wrong — the most useful line in the whole practice for the *next* decision.

## Signal

Proposals declare metrics with baselines and targets and nobody looks at the actual values. Or the same optimistic assumption appears in a third proposal.

## Adds

**A document**: `outcome.md` in an initiative directory, or `<slug>-outcome.md` next to a proposal that declared a metric. One page:

```
# [name] — Outcome review
## Requirements
| Metric | Baseline | Target | Actual (T+30) | Verdict |     (met / missed / not measurable)
## Outcome
- Predictions that held:
- Predictions that failed, and why:
- Accepted risks that materialized:
## What we learned          (for the next initiative, not this one; three at most)
## Follow-ups               (each linked to an issue or a new proposal)
## Process retrospective    (was the sizing right? was the document read? two lines)
```

**A schedule**: written at T+30 days after launch; a T+90 section appended if the metrics had not settled. With `proposal-metadata`, `review_on:` in the front matter carries the date.

**An authorship rule**: metric collection may be done by an assistant; "what we learned" is written by a person.

## Rules

| ID | Rule | Principle |
|---|---|---|
| **OR1** | An initiative MUST have an outcome review at T+30; any proposal that declared a metric MAY. | P2 |
| **OR2** | The review MUST compare each declared metric with its baseline and target, and MUST record which predictions held, which failed and why, and which accepted risks materialized. | P2 |
| **OR3** | An outcome review is immutable once written, except that a T+90 section MAY be appended. | P4 |
| **OR4** | "What we learned" MUST be written by a person. | P5 |

## Parameters

Days after launch (default 30; follow-up 90). Which proposals require one (default: initiatives).

## Cost

One page per initiative, thirty days late — the hardest kind of task to remember, which is why the date lives in front matter.

## Remove

Stop scheduling; existing reviews remain. Metrics revert to decoration.
