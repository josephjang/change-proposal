# Pattern: proposal-metadata

Gives a proposal machine-readable identity and state, who owns it, what state it is in, which pull requests and issue it belongs to, which areas it touches, without putting any of that in the prose.

**When.** Proposals need to be found by something other than their date and title (an area, an owner, a status), or a change spans more than one pull request and readers cannot tell whether the proposal describes finished work.

**Goes with.** `supersession` (uses `status`, adds two fields), `agent-context` (uses `touches`), `sizing-tiers` (adds `tier`), `design-first-review` (adds a status value), `initiative-umbrella` (adds `parent`), `lint-gate` (validates the block).

## What it adds

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

**A status set** other patterns extend: `supersession` adds `superseded`; `design-first-review` adds `accepted`; `spike-then-spec` adds `abandoned`.

**An id form**, when one is wanted: `CP-` followed by the file name without extension, so the id and the path always agree.

## Using it

- Keys and values are English regardless of the body's language; this matters once `multilingual-records` is on.
- `status` moves from `draft` to `implemented` in the pull request that completes the work. For a single-PR change that is the same PR that adds the file. A proposal on the main branch whose work is complete says `implemented`; a stale `draft` is the most common defect.
- Each pull request that implements part of the proposal appends itself to `prs`.

## Cost

Seven lines per proposal, and the discipline of flipping `status` when the last PR merges.

## Removing it

Stop adding the block. Existing blocks are harmless. Patterns that need this one (`supersession`, `agent-context`, `sizing-tiers`, `design-first-review`, `initiative-umbrella`) go first or lose their fields.
