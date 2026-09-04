# Pattern: human-ai-split

- **Requires**: core
- **Combines with**: `evidence-verification` (together they define what an assistant may and may not write), `before-after` (its `Change` section is the typical assistant-drafted section), `agent-context` (the instruction block carries these rules), `lint-gate` (markers are checked)
- **Conflicts with**: —

## Intent

Let an AI assistant do all the drafting it is good at while making it impossible for the judgment in a proposal to have been authored by no one.

## Signal

An assistant is used to write any part of a proposal.

## Adds

**A classification of sections.** An assistant may draft either kind; the classification says what a person must do before the marker comes off.

| Judgment — a person decides | Derived — a person reads |
|---|---|
| `Problem`, `Goals`, `Non-Goals`, `Requirements`, `Decisions` (or `Product Decisions` / `Technical Decisions`), `Risks`, the rollback line of `Rollout & rollback` | `Change`, `Summary`, `Cross-cutting concerns`, `Verification` (only what was run — see `evidence-verification`), `Living docs` |

A drafted judgment section must **expose its decision points** — what it assumed, which alternatives it considered and rejected — so the person approves a decision, not prose. The person makes it theirs by editing it, or by deciding it stands as written. For a derived section, reading is enough.

**A marker.** `<!-- ai-draft -->` directly under every section an assistant drafted. A person removes it — after deciding, for a judgment section; after reading, for a derived one. The removal commit is the per-section approval record. A marker left in a merged proposal is a defect.

**A front-matter field** (with `proposal-metadata`): `ai_assisted: true | false`, for later analysis. Not a quality signal.

**An instruction to assistants**, placed wherever the repository instructs them (its agent file, or the `agent-context` block):

> Leave `<!-- ai-draft -->` under every section you draft. When drafting a judgment section, state its decision points — what you assumed, which alternatives you rejected and why — and ask the person to decide or approve; never present settled-looking prose that hides an open decision. Never remove a marker. Never translate, rewrite or "improve" a person's text in a judgment section.

**One line in the reviewer's checklist**: every judgment section was written or approved by a person; no marker remains.

## Rules

| ID | Rule |
|---|---|
| **HA1** | A section drafted by an assistant MUST carry `<!-- ai-draft -->` until a person has read it — for a judgment section, until the person has edited it or decided it stands. |
| **HA2** | No marker MAY remain in a proposal at merge. |
| **HA3** | An assistant MAY draft any section. A drafted judgment section MUST expose its decision points — what was assumed, which alternatives were rejected — so the person approves a decision, not prose. |
| **HA4** | An assistant MUST NOT translate, rewrite or improve a person's text in a judgment section. |
| **HA5** | With `proposal-metadata`, `ai_assisted` SHOULD be set. |

## Cost

A few minutes of deciding and reading per proposal, which the person should be spending anyway.

## Remove

Drop the marker and the checklist line. A team that removes this pattern while still using assistants to draft has decided to trust assistant-authored judgment; that decision deserves a proposal of its own.
