# Pattern: verification

**Candidate.** Not validated, and not written ahead of its situation either: this section was part of the core until the first adoption's findings moved it out. It may be validated by use, absorbed back into the core, or dropped. See [the catalog](README.md).

Records in the proposal what was checked and what was observed, and what was *not* checked, which no pull request or tracker keeps.

**When.** "Was this actually tested?" is asked after the merge and the answer lives only in CI logs or a chat scroll; or an unchecked path surfaces as a surprise because no record said it was not checked.

**Goes with.** `evidence-verification` (fixes this section's strict form), `human-ai-split` (`Verification` is a derived section), `lint-gate` (the "not checked" line is checked), `agent-skills` (`cp-finish` fills it).

## What it adds

**One section**, placed after `Decisions`:

```
## Verification
- Checked: (what was checked and what was observed)
- Not checked, and why:
```

The "not checked" half is the part nothing else records; the pull request and the tracker usually hold the rest. That asymmetry is why the section lives in the proposal.

## Using it

- Say what was checked and what was observed, not what was done. "Ran the tests" is a claim; "14 passed, 9 new" is an observation.
- Always say what was not checked, and why. That line is the reason the section exists.

## Cost

A few lines written at finish time, when the answer is freshest, plus the discipline of admitting what was not checked.

## Removing it

Drop the section from the template. What was verified reverts to the PR description; what was not checked is recorded nowhere.
