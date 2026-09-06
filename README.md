# change-proposal

A practice for recording the *intent and judgment* behind a change to a product or system.

A **change proposal** records why a change is being made, what it deliberately leaves out, what was decided and rejected, and what risks were knowingly accepted. It is started before the work and finished with it: whoever builds the change, a person or an AI assistant, builds it from the proposal, and after the merge the proposal is the change's record.

## Where to read

| Path | What |
|---|---|
| [`docs/guide.md`](docs/guide.md) | The practice, explained once: what a proposal is, when to write one, what goes in each section and why, what it is not, and how to go beyond it |
| [`templates/change-proposal.md`](templates/change-proposal.md) | The template |
| `docs/changes/` | This repository's own proposals; it uses the practice on itself |

## The practice in five lines

1. A change that alters observable behavior gets a proposal at `docs/changes/YYYY-MM-DD-<slug>.md`, in the same PR as the code. No behavior change: the PR description says so.
2. The proposal has six sections, **Problem**, **Goals**, **Non-Goals**, **Requirements**, **Decisions**, **Risks**, plus an optional **Summary** up top.
3. It is what the change is built from, by a person or an AI assistant, and it records what the code cannot: why, what was left out, what was rejected and why, what was knowingly accepted.
4. A person or an AI assistant writes it. Empty sections are deleted.
5. Nothing else is required. When you meet a situation the practice does not cover, write the smallest addition that answers it, and tell us how it went.
