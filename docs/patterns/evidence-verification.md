# Pattern: evidence-verification

- **Requires**: core, `verification` (the section this pattern strictifies)
- **Combines with**: `human-ai-split` (Verification is a derived section; this pattern says what may go in it), `lint-gate` (the "not done" entry is checked)
- **Conflicts with**: —

## Intent

Make the `Verification` section a list of evidence rather than a list of claims, so that a reader — or an agent building on the change — can tell what is actually known to work.

## Signal

An assistant implements or tests any part of a change. Also: a reviewer catches a "verified" line that turns out not to have been run.

## Adds

**The strict shape of the section.** The `verification` pattern asks for "what was checked and observed; what was not, and why". This pattern fixes the form:

```
## Verification
- Automated: `<command>` → <observed result>
- Manual: <what was done, in which environment, what was observed>
- Not done, and why: <what was not verified, and the reason>
```

**A reviewer test**: could this line have been written by someone who did not run the check? (`tests pass` — yes. `pytest tests/x -k retry → 14 passed, 9 new` — no.) Does the manual line name an environment and an observation? Is "Not done, and why" present and honest?

**An instruction to assistants**: an unrun check described as verified is a defect in the output, not a style issue.

## Rules

| ID | Rule | Principle |
|---|---|---|
| **EV1** | `Verification` MUST list only commands that were executed with their observed results, and manual checks that were actually performed, with environment and observation. | P6 |
| **EV2** | `Verification` MUST contain a "Not done, and why" entry. It MAY say "nothing" with a reason; it MUST NOT be omitted. | P6 |
| **EV3** | A reviewer MUST reject a Verification section that reads as a claim rather than as evidence. | P6 |
| **EV4** | An assistant that did not run a check MUST NOT describe it as verified. | P6 |

## Cost

None beyond honesty. Fluent drafts get rejected more often at first; that is the pattern working.

## Remove

Drop EV1–EV4; the `verification` pattern's looser wording remains. Removing it while assistants implement code means accepting their verification claims at face value.
