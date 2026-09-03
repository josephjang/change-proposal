# Pattern: agent-skills

- **Requires**: core; `agent-context` for the context skill; `human-ai-split` and `evidence-verification` for the drafting and finishing skills; `supersession` for the reversal skill
- **Combines with**: every pattern whose steps are mechanical
- **Conflicts with**: —

## Intent

Package the mechanical parts of the practice — finding constraints, scaffolding a proposal, sizing, finishing, reviewing, reversing — as skills that Claude Code and Codex can run, so the same procedure is not pasted into every session.

## Signal

The same multi-step instructions are being pasted into agent sessions repeatedly, or agents perform the steps inconsistently across sessions.

## Adds

**Skill specifications.** This pattern specifies what each skill must do; it does not ship them. An adopter writes them in the portable Agent Skills format — a directory per skill with a `SKILL.md` whose frontmatter uses only `name`, `description` and optionally `metadata`, which both Claude Code (`.claude/skills/<name>/`) and Codex (`.agents/skills/<name>/`) accept — and records their behavior in a proposal.

| Skill | Must do | Must not do |
|---|---|---|
| `cp-context` | Find proposals whose `touches` or paths overlap the task; classify by status; extract `Decisions` (split or not), `Non-Goals`, `Risks`; report *compatible / careful / would reverse* per constraint; stop and ask if the task would reverse one. | Summarize proposals it did not open; proceed silently on a reversal. |
| `cp-draft` | Create the file at the right path from the repository's template; collect judgment sections by asking one question at a time and recording the person's words; draft derived sections with markers; add the sections the adopted patterns require; report what the person still owns. | Write a judgment section as a conclusion; remove a marker; translate a person's text. |
| `cp-size` | Answer "does behavior change?", then the three risk signals or the tier rubric, each with one line of reasoning; state the consequences (sections, pre-code review); produce the PR line. | Size by diff length, time, or who wrote the code. |
| `cp-finish` | Fill `Change` from the diff; fill `Verification` only with commands run in the session and their output; move everything else to "Not done, and why"; list markers remaining, word count, living docs; prepare the PR description. | Describe an unrun check as verified; edit a person's text; edit a merged proposal. |
| `cp-review` | Walk the core rules and the rules of adopted patterns; run the lint if present; report blocking and non-blocking comments with rule ids and questions for the author. | Fix the author's judgment sections; recommend adopting patterns inside a review. |
| `cp-supersede` | Create the new proposal with `supersedes`; set the old proposal's `status` and `superseded_by` and nothing else; handle reverts and partial reversals. | Edit the old body; delete anything. |

**Conventions every skill follows**: read the composition from `docs/changes/README.md` first and do nothing a non-adopted pattern would require; draft in the record language; end with a list of what was left for the person.

## Rules

| ID | Rule | Principle |
|---|---|---|
| **AS1** | A skill MUST read the repository's composition before acting and MUST NOT perform steps of a pattern the repository has not adopted. | P10 |
| **AS2** | A skill MUST NOT remove a `<!-- ai-draft -->` marker, write a judgment section as a conclusion, or describe an unrun check as verified. | P5, P6 |
| **AS3** | A skill MUST NOT edit a proposal whose status is `implemented` or `superseded`, except `cp-supersede` setting the two permitted fields. | P4 |
| **AS4** | A change to a skill MUST be recorded as a proposal whose `Verification` names the tool and version it was exercised in. | P6 |

## Cost

Writing and maintaining the skills; verifying them in each tool as tools change.

## Remove

Delete the skill directories. The procedures remain described here and in the other cards.
