# Pattern: proposal-metadata

- **Requires**: core
- **Combines with**: `supersession` (uses `status`, adds two fields), `agent-context` (uses `touches`), `sizing-tiers` (adds `tier`), `design-first-review` (adds a status value), `initiative-umbrella` (adds `parent`), `lint-gate` (validates the block)
- **Conflicts with**: —

## Intent

Give a proposal machine-readable identity and state — who owns it, what state it is in, which pull requests and issue it belongs to, which areas it touches — without putting any of that in the prose.

## Signal

Proposals need to be found by something other than their date and title (an area, an owner, a status), or a change spans more than one pull request and readers cannot tell whether the proposal describes finished work.

## Adds

**A front-matter block** at the top of the file:

```yaml
---
title:                # one line; the H1 may repeat it
status: draft         # draft | implemented   (other patterns add values)
owner: "@"
date: YYYY-MM-DD
issue:                # link, optional
prs: []               # every pull request that implements the proposal
touches: []           # area tags, free-form until agent-context sets a vocabulary
---
```

**Two conventions**: keys and values are English regardless of the body's language (this matters once `multilingual-records` is on); `status` moves from `draft` to `implemented` in the pull request that completes the work — for a single-PR change, the same PR that adds the file.

**A status set** other patterns extend: `supersession` adds `superseded`; `design-first-review` adds `accepted`; `spike-then-spec` adds `abandoned`.

## Rules

| ID | Rule | Principle |
|---|---|---|
| **PM1** | A proposal MUST begin with front matter containing `title`, `status`, `owner`, `date`, `prs`, `touches`. Keys and values MUST be English. | P7 |
| **PM2** | `status` MUST be `draft` or `implemented`, plus values introduced by adopted patterns. A proposal on the main branch whose work is complete MUST be `implemented`. | P3, P7 |
| **PM3** | Each pull request that implements part of the proposal MUST append itself to `prs`. | P3 |
| **PM4** | An `id`, when used, MUST be `CP-` followed by the file name without extension. | P7 |

## Cost

Seven lines per proposal, and the discipline of flipping `status` when the last PR merges.

## Remove

Stop adding the block. Existing blocks are harmless. Patterns that require this one (`supersession`, `agent-context`, `sizing-tiers`, `design-first-review`, `initiative-umbrella`) must be removed first or lose their fields.
