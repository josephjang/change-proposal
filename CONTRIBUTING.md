# Contributing

This repository uses the practice on itself. Its proposals live in `docs/changes/`; what it uses beyond the [guide](docs/guide.md) is stated at the top of `docs/changes/README.md`.

## What needs a proposal

A change to what the practice asks for: when a proposal is needed, which sections it has and what they hold, what a pattern adds or when it applies, what the template asks for, or a new section name. Validating a [candidate pattern](docs/patterns/README.md#adding-validating-absorbing-retiring), absorbing it into the core, or retiring it is such a change too. Every adopter inherits these, so the reasoning is worth a record.

Wording, examples and typos do not; the PR description is enough.

Neither does an adoption report, the account of what a candidate did for a team that ran it. It arrives as a pull request against the pages of the candidates it concerns, and the PR description is enough. Say which candidates you adopted, how long you ran them, which of them earned their place, which turned out to be ceremony, and where the page or the guide was wrong. Each adopted candidate's page gets one entry, at the end of the page, under an `## Adoption reports` heading that follows `## Removing it` and that the first report on that page creates:

```
## Adoption reports

### <who you are>, <how long you ran it>

<what you found, in your own words>
```

Everything above that heading is this repository's prose; the report is yours, stays in your voice and under your name, and is not rewritten into the page's. You are not asked for a verdict. The proposal that validates a candidate, absorbs it into the core or retires it is written later, by the maintainer, from the reports that have accumulated. `docs/patterns/verification.md` and `docs/patterns/human-ai-split.md` already carry adoption findings inline, in the `**Candidate.**` line at the top of the page; those are the maintainer's own record of what has been learned, and an adoption report is the same evidence in the adopter's words.

## How

1. Read the existing proposals in `docs/changes/`; the reasoning behind the current shape is there.
2. Start from `templates/change-proposal.md`. The `Problem` names the situation the current practice mishandled, ideally one somebody met. A proposal that starts from a solution is sent back.
3. For a new pattern: name the situation it answers, what it adds, and what every change pays while it is on. For validating, absorbing or retiring a candidate: name the adoptions that showed it, which are the reports its page has collected. This repository's own use of a candidate is not one of them: it wrote the candidates, and its changes are changes to the practice rather than to a product, so what it learns here can motivate a proposal but is not evidence that settles one.

## Reviewing

The reviewer asks one question of every substantive change: *what does this make easier to understand or to do, and what does it cost?* A change that only adds a constraint, with no situation behind it, is declined. The practice is still too young to be tightened on anticipation.
