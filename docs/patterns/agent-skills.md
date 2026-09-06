# Pattern: agent-skills

**Candidate.** Written before anyone met its situation; not validated. It may be validated by use, absorbed into the core, or dropped. See [the catalog](README.md).

Packages the mechanical parts of the practice, finding constraints, scaffolding a proposal, sizing, finishing, reviewing, reversing, as skills that Claude Code and Codex can run, so the same procedure is not pasted into every session.

**When.** The same multi-step instructions are being pasted into agent sessions repeatedly, or agents perform the steps inconsistently across sessions.

**Needs.** `agent-context` for the context skill; `human-ai-split` and `evidence-verification` for the drafting and finishing skills; `supersession` for the reversal skill. Goes with every pattern whose steps are mechanical.

## What it adds

**Skill descriptions.** This pattern says what each skill should do; it does not ship them. An adopter writes them in the portable Agent Skills format, a directory per skill with a `SKILL.md` whose frontmatter uses only `name`, `description` and optionally `metadata`, which both Claude Code (`.claude/skills/<name>/`) and Codex (`.agents/skills/<name>/`) accept, and records their behavior in a proposal.

| Skill | Does | Does not |
|---|---|---|
| `cp-context` | Find proposals whose `touches` or paths overlap the task; classify by status; extract `Decisions` (split or not), `Non-Goals`, `Risks`; report *compatible / careful / would reverse* per constraint; stop and ask if the task would reverse one. | Summarize proposals it did not open; proceed silently on a reversal. |
| `cp-draft` | Create the file at the right path from the repository's template; draft sections with markers, exposing each judgment section's decision points and asking the person to decide or approve; add the sections the patterns in use call for; report what the person still owns. | Remove a marker; hide an open decision inside settled-looking prose; translate a person's text. |
| `cp-size` | Answer "does behavior change?", then the three risk signals or the tier rubric, each with one line of reasoning; state the consequences (sections, pre-code review); produce the PR line. | Size by diff length, time, or who wrote the code. |
| `cp-finish` | Fill `Change` from the diff; fill `Verification` only with commands run in the session and their output; move everything else to "Not done, and why"; list markers remaining, word count, living docs; prepare the PR description. | Describe an unrun check as verified; edit a person's text; edit a merged proposal. |
| `cp-review` | Walk the guide and the pages of the patterns in use; run the lint if present; report blocking and non-blocking comments with questions for the author. | Fix the author's judgment sections; recommend adopting patterns inside a review. |
| `cp-supersede` | Create the new proposal with `supersedes`; set the old proposal's `status` and `superseded_by` and nothing else; handle reverts and partial reversals. | Edit the old body; delete anything. |

**Conventions every skill follows.** Read which patterns the repository uses from `docs/changes/README.md` first, and do nothing a pattern not in use would call for. Never remove a `<!-- ai-draft -->` marker, draft a judgment section without exposing its decision points, or describe an unrun check as verified. Never edit a proposal whose status is `implemented` or `superseded`, except `cp-supersede` setting the two fields it owns. Draft in the record language. End with a list of what was left for the person.

## Using it

A change to a skill changes the practice as the team experiences it. Record it as a proposal whose `Verification` names the tool and version the skill was exercised in.

## Cost

Writing and maintaining the skills; verifying them in each tool as tools change.

## Removing it

Delete the skill directories. The procedures remain described here and on the other pattern pages.
