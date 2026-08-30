# Pattern: human-ai-split

- **Requires**: core
- **Combines with**: `evidence-verification` (together they define what an assistant may and may not write), `before-after` (its `Change` section is the typical assistant-drafted section), `agent-context` (the instruction block carries these rules), `lint-gate` (markers are checked)
- **Conflicts with**: —

## Intent

Let an AI assistant do all the drafting it is good at while making it impossible for the judgment in a proposal to have been authored by no one.

## Signal

An assistant is used to write any part of a proposal.

## Adds

**A classification of sections.**

| Judgment — a person writes or confirms | Derived — an assistant may draft |
|---|---|
| `Problem`, `Non-goals` (or `Goals / Non-goals`), `Success criteria`, `Decisions`, `Risks & deferred`, the rollback line of `Rollout & rollback` | `Change`, `Summary`, `Cross-cutting concerns`, `Verification` (only what was run — see `evidence-verification`), `Living docs` |

For judgment sections the assistant **supplies material** — alternatives it tried, risks it noticed, a digest of the issue — and asks for the conclusion. It does not write the conclusion.

**A marker.** `<!-- ai-draft -->` directly under every section an assistant drafted. A person removes it after reading; the act of removal is the confirmation. A marker left in a merged proposal is a defect.

**A front-matter field** (with `proposal-metadata`): `ai_assisted: true | false`, for later analysis. Not a quality signal.

**An instruction to assistants**, placed wherever the repository instructs them (its agent file, or the `agent-context` block):

> Draft only the derived sections, and leave `<!-- ai-draft -->` under each. For judgment sections, offer material and ask; never write the conclusion. Never translate, rewrite or "improve" a person's text in a judgment section.

**One line in the reviewer's checklist**: judgment sections were written by a person; no marker remains.

## Rules

| ID | Rule | Principle |
|---|---|---|
| **HA1** | A section drafted by an assistant MUST carry `<!-- ai-draft -->` until a person has read it. | P5 |
| **HA2** | No marker MAY remain in a proposal at merge. | P5 |
| **HA3** | An assistant MUST NOT author a judgment section as a conclusion. It MAY supply material and MUST ask the person for the conclusion. | P5 |
| **HA4** | An assistant MUST NOT translate, rewrite or improve a person's text in a judgment section. | P5 |
| **HA5** | With `proposal-metadata`, `ai_assisted` SHOULD be set. | P5 |

## Cost

A few minutes of reading per proposal, which the person should be spending anyway.

## Remove

Drop the marker and the checklist line. A team that removes this pattern while still using assistants to draft has decided to trust assistant-authored judgment; that decision deserves a proposal of its own.
