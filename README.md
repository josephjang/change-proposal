# change-proposal

A practice for recording the *intent and judgment* behind a change to a product or system.

A **Change Proposal** records why a change is being made, what it deliberately leaves out, what was decided and rejected, and what risks were knowingly accepted. It is started before the work and finished with it: whoever builds the change, a person or an AI assistant, builds it from the proposal, and after the merge the proposal is the change's record.

A proposal has two forms. A **Unified Change Proposal** keeps the change in one concise document, suitable for small, straightforward feature additions and changes. A **Split Change Proposal** separates **Product Requirements** and **Technical Design** into two documents so each aspect can be developed and reviewed independently. Both forms are complete Change Proposals; the names describe document organization, not levels of rigor.

## Where to read

| Path | What |
|---|---|
| [`docs/guide.md`](docs/guide.md) | The practice: what a proposal is, which form to use, what belongs in it, and how it follows the change |
| [`templates/change-proposal.md`](templates/change-proposal.md) | The Unified form: the original single-document template for ordinary changes |
| [`docs/split-proposals.md`](docs/split-proposals.md) | The Split form: responsibilities, independent reviews, templates for both documents, and examples from TarkovHelper |
| [`examples/README.md`](examples/README.md) | Filled-in Unified and Split examples for a fictional notes app, in English with Korean editions and a suggested reading order |
| `docs/changes/` | This repository's own proposals; it uses the practice on itself |

## The practice in five lines

1. A change that alters observable behavior gets a proposal in the same PR as the code. No behavior change: the PR description says so.
2. Use the Unified form, the original six-section document, for small, straightforward changes. For technically complex changes, use the Split form: Product Requirements and Technical Design as two parts of one proposal.
3. Start the proposal before implementation and finish it with the work. It records intent, scope, requirements, decisions, and risks, with technical design where needed.
4. Review the product and technical aspects independently when separated, then check that the requirements and design agree. Each requirement and rationale has one authoritative home.
5. Keep the documents alongside the code. After merge they record the judgment of the time; live progress belongs in PRs or issues.
