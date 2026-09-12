# Worked examples

English | [한국어](README.ko.md)

These are filled-in examples of the two Change Proposal forms, using a fictional personal-notes app. They are maintained learning material, not this repository's implementation records, approved product plans, or evidence of executed tests. English is the default; Korean editions use matching `.ko.md` files. Both editions keep the templates' English section names and the same requirement and decision IDs. Links within each Split pair stay in that language, and each document links to its counterpart in the other language.

| Form | Example | Why this form fits |
|---|---|---|
| Unified | [Clear note search](2026-09-12-clear-note-search.md) | A small UI change reuses an existing search flow. Intent, acceptance criteria, and the few consequential choices fit in one document. |
| Split | Note trash and 30-day restoration: [Product Requirements](2026-09-12-note-trash.requirements.md) + [Technical Design](2026-09-12-note-trash.design.md) | The user promise needs separate treatment from expiry, concurrent restoration and cleanup, access boundaries, and data migration. |

## How to read them

1. Read the Unified example first. Its six sections are the complete proposal. The optional Summary is omitted because the change is short; there is no missing design document.
2. Read the Split example's Product Requirements on its own: should this behavior exist, and are its scope and promises right? Then read Technical Design: can this design meet those requirements safely?
3. Follow R3 from the product promise of restoring the original note to the technical choice of keeping its ID and content, and then to its planned check in Test Strategy. Verification explicitly says that no implementation tests ran.

Both examples describe independent changes, not successive stages or a requirement to write both forms for one change. Their shared fictional app makes the difference in review needs easier to see. Choosing a form depends on the decisions and review it needs, not the document's length.

The Korean editions are [Clear note search](2026-09-12-clear-note-search.ko.md), [Product Requirements](2026-09-12-note-trash.requirements.ko.md), and [Technical Design](2026-09-12-note-trash.design.ko.md). They translate the same proposals, not additional changes. Update both languages together when the example's behavior, assumptions, or decisions change.

This page is the examples catalog, not a third component of the Split proposal. Its two linked documents are the whole proposal. Each sample states its assumptions; an actual proposal would replace those assumptions with inspected repository evidence and real verification results where applicable.

Use the [main guide](../docs/guide.md#choosing-a-form) to choose a form and the [Split guide](../docs/split-proposals.md) for the pair's responsibilities. Copy a [Unified](../templates/change-proposal.md), [Product Requirements](../templates/product-requirements.md), or [Technical Design](../templates/technical-design.md) template when writing your own change, rather than adopting the examples' product policies by default. This repository's actual changes remain under [docs/changes](../docs/changes/).
