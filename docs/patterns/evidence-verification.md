# Pattern: evidence-verification

Makes the `Verification` section a list of evidence rather than a list of claims, so that a reader, or an agent building on the change, can tell what is actually known to work.

**When.** An assistant implements or tests any part of a change. Also: a reviewer catches a "verified" line that turns out not to have been run.

**Needs.** `verification` (the section this pattern tightens). Goes with `human-ai-split` (Verification is a derived section; this pattern says what may go in it) and `lint-gate` (the "not done" entry is checked).

## What it adds

**The strict shape of the section.** The `verification` pattern asks for "what was checked and observed; what was not, and why". This pattern fixes the form:

```
## Verification
- Automated: `<command>` → <observed result>
- Manual: <what was done, in which environment, what was observed>
- Not done, and why: <what was not verified, and the reason>
```

**A reviewer test.** Could this line have been written by someone who did not run the check? (`tests pass`: yes. `pytest tests/x -k retry → 14 passed, 9 new`: no.) Does the manual line name an environment and an observation? Is "Not done, and why" present and honest?

**An instruction to assistants.** An unrun check described as verified is a defect in the output, not a style issue.

## Using it

- `Verification` lists only commands that were executed, with their observed results, and manual checks that were actually performed, with environment and observation.
- "Not done, and why" is always present. It may say "nothing" with a reason; it is not omitted.
- A reviewer sends back a Verification section that reads as a claim rather than as evidence. Fluent drafts get rejected more often at first; that is the pattern working.

## Cost

None beyond honesty.

## Removing it

The `verification` pattern's looser wording remains. Removing this while assistants implement code means accepting their verification claims at face value.
