# Pattern: outcome-review

Closes the loop on the metrics a proposal declared, and records where the prediction was wrong: the most useful line in the whole practice for the *next* decision.

**When.** Proposals declare metrics with baselines and targets and nobody looks at the actual values. Or the same optimistic assumption appears in a third proposal.

**Needs.** A declared metric in `Requirements` to compare against. Goes with `initiative-umbrella` (always on for initiatives), `supersession` (an outcome is immutable once written), `proposal-metadata` (a `review_on` date).

## What it adds

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

**A schedule.** Written at T+30 days after launch; a T+90 section appended if the metrics had not settled. With `proposal-metadata`, `review_on:` in the front matter carries the date, because thirty-days-later is the hardest kind of task to remember.

## Using it

- An initiative always gets an outcome review; any proposal that declared a metric may.
- The review compares each declared metric with its baseline and target, and records which predictions held, which failed and why, and which accepted risks materialized.
- Once written it is not edited, except that a T+90 section may be appended.
- Metric collection may be done by an assistant. "What we learned" is written by a person.

## Knobs

Days after launch (default 30; follow-up 90). Which proposals get one (default: initiatives).

## Cost

One page per initiative, thirty days late.

## Removing it

Stop scheduling; existing reviews remain. Metrics revert to decoration.
