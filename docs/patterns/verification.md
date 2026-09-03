# Pattern: verification

- **Requires**: core
- **Combines with**: `evidence-verification` (fixes this section's strict form; requires this pattern), `human-ai-split` (`Verification` is a derived section), `lint-gate` (the "not checked" line is checked), `agent-skills` (`cp-finish` fills it)
- **Conflicts with**: —

## Intent

Record in the proposal what was checked and what was observed — and what was *not* checked, which no pull request or tracker keeps.

## Signal

"Was this actually tested?" is asked after the merge and the answer lives only in CI logs or a chat scroll; or an unchecked path surfaces as a surprise because no record said it was not checked.

## Adds

**One section**, placed after `Decisions`:

```
## Verification
- Checked: (what was checked and what was observed)
- Not checked, and why:
```

The "not checked" half is the part nothing else records; the pull request and the tracker usually hold the rest. That asymmetry is why the section lives in the proposal.

## Rules

| ID | Rule | Principle |
|---|---|---|
| **V1** | `Verification` MUST state what was checked and what was observed, and MUST state what was not checked, with the reason. | P6 |

## Cost

A few lines written at finish time, when the answer is freshest — plus the discipline of admitting what was not checked.

## Remove

Drop the section from the template. What was verified reverts to the PR description; what was not checked reverts to nowhere, which is the reason to keep it.
