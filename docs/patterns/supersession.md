# Pattern: supersession

Keeps every merged proposal an honest record of the judgment of its time, and makes "is this proposal still current?" answerable from one file's front matter.

**When.** The first time someone wants to "fix" a merged proposal. Adopting it before that moment is cheaper than arguing it then.

**Needs.** `proposal-metadata` (for `status` and the two fields below). Goes with `agent-context` (agents rely on `status` and `superseded_by` to judge validity), `living-docs-bridge` (the bridge that makes immutability bearable), `lint-gate` (immutability is checked against a base ref).

## What it adds

**Two front-matter fields** and **one status value**:

```yaml
supersedes:       # in the new proposal: id of the one it reverses
superseded_by:    # in the old proposal: id of the one that reversed it; the only post-merge edit
status: superseded
```

**A procedure.** To reverse a merged proposal, in whole or in part: write a new proposal whose `Problem` says what is being reversed and which facts changed; set its `supersedes`; in the same pull request set the old proposal's `status: superseded` and `superseded_by`; leave the old body untouched. Reverts carry a proposal of their own and supersede the reverted one; re-applying later supersedes both.

**A reading rule.** `implemented` is current. `superseded` is history; read the proposal that `superseded_by` points to instead.

## Using it

- The body of an `implemented` or `superseded` proposal is not edited. The only front-matter edits after merge are `status` → `superseded` and `superseded_by`.
- A partial reversal follows the same procedure and says in `Problem` which part is reversed.
- A revert pull request carries a proposal; the reverted proposal becomes `superseded`.
- Corrections of substance to a merged proposal are made as a new proposal. Typos are left alone; the record is the record.
- One review reflex: "this PR edits a merged proposal" is a rejection.

## Cost

An occasional extra proposal for a correction.

## Removing it

Allow edits to merged proposals. That is coherent for a repository that treats proposals as living documents, but it is incompatible with `agent-context`: agents can no longer tell whether a proposal reflects the current decision without reading history. Remove that pattern too, or keep this one.
