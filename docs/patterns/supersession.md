# Pattern: supersession

- **Requires**: core, `proposal-metadata` (for `status` and the two fields below)
- **Combines with**: `agent-context` (agents rely on `status` and `superseded_by` to judge validity), `living-docs-bridge` (the bridge that makes immutability bearable), `lint-gate` (immutability is checked against a base ref)
- **Conflicts with**: editing merged proposals in place

## Intent

Keep every merged proposal an honest record of the judgment of its time, and make "is this proposal still current?" answerable from one file's front matter.

## Signal

The first time someone wants to "fix" a merged proposal. Adopting it before that moment is cheaper than arguing it then.

## Adds

**Two front-matter fields** and **one status value**:

```yaml
supersedes:       # in the new proposal: id of the one it reverses
superseded_by:    # in the old proposal: id of the one that reversed it — the only post-merge edit
status: superseded
```

**A procedure.** To reverse a merged proposal, in whole or in part: write a new proposal whose `Problem` says what is being reversed and which facts changed; set its `supersedes`; in the same pull request set the old proposal's `status: superseded` and `superseded_by`; leave the old body untouched. Reverts carry a proposal of their own and supersede the reverted one; re-applying later supersedes both.

**A reading rule.** `implemented` is current. `superseded` is history — read the proposal that `superseded_by` points to instead.

## Rules

| ID | Rule | Principle |
|---|---|---|
| **SU1** | The body of a proposal whose status is `implemented` or `superseded` MUST NOT be edited. The only permitted front-matter edits are `status` → `superseded` and `superseded_by`. | P4 |
| **SU2** | A proposal that reverses a merged proposal MUST set `supersedes`, and the same pull request MUST set the old proposal's `status` and `superseded_by`. Partial reversals follow the same rule and say in `Problem` which part is reversed. | P4 |
| **SU3** | A revert pull request MUST carry a proposal; the reverted proposal becomes `superseded`. | P4 |
| **SU4** | Corrections of substance to a merged proposal MUST be made as a new proposal. Typos SHOULD be left alone. | P4 |

## Cost

An occasional extra proposal for a correction, and one review reflex: "this PR edits a merged proposal" is a rejection.

## Remove

Allow edits to merged proposals. That is coherent for a repository that treats proposals as living documents, but it is incompatible with `agent-context` — agents can no longer tell whether a proposal reflects the current decision without reading history. Remove that pattern too, or keep this one.
