# Principles

Five principles. Each has a statement, the reasoning, what it implies, and the tension it creates. When a rule and a principle conflict in a concrete case, the principle wins and the rule needs a proposal.

The principles describe the whole practice, patterns included. Where a principle's implication is carried by a pattern rather than by the core, the pattern is named — and until a team adopts that pattern, the principle is guidance, not a rule.

---

## P1. Proportionality — document by blast radius, not by diff size

**Statement.** How much a change needs to be documented is set by who and what it can affect and by how hard it is to reverse — never by how many lines changed, how long it took, or whether a person or an assistant wrote the code.

**Reasoning.** Diff size correlates badly with risk, and the correlation collapses entirely when assistants produce thousands of correct mechanical lines in minutes. A permission check is one line.

**Implies.** The core's only sizing question is "does behavior change?". Finer sizing — pre-code review for risky changes, explicit tiers — is `risk-signals` and `sizing-tiers`.

**Tension.** Blast radius takes judgment; diff size is free. Teams drift back to diff size unless the questions are few and the edge cases are written down.

## P2. Judgment over description — write what code cannot say

**Statement.** A proposal holds only what cannot be recovered from the code, the tests or the tracker: why, what was left out, what was rejected, what was accepted, what was observed. Anything with a source of truth elsewhere is referenced, not copied.

**Reasoning.** Copied description goes stale the day after merge and teaches readers to distrust the document. Judgment does not go stale; it is a fact about the past.

**Implies.** No schemas, payloads, file lists or work breakdowns in a proposal. Rejection reasons of the kind that would change if the facts changed. A number used as evidence carries its re-measurement method, or is restated in terms that stay true as time passes. The six required core sections are all judgment.

**Tension.** Describing is easier than judging, and assistants are excellent at describing. Templates must refuse description.

## P3. Co-location — the proposal rides with the code

**Statement.** A proposal lives in the repository, in the same pull request, review and history as the change.

**Reasoning.** A document that must be found elsewhere is not read — by people or by agents. Reviewing the change and reviewing its reasoning are one act.

**Implies.** `docs/changes/` and the same PR. Approval is PR approval; there is no status box in the document.

**Tension.** Non-engineering stakeholders may not live in the repository. Render or mirror; never move the source of truth.

## P4. Immutability — a merged proposal is a record of its time

**Statement.** Once merged, a proposal records the judgment of that moment. Later knowledge is recorded in a later proposal, not written over the old one.

**Reasoning.** Overwriting the judgment of the time erases "why we thought so then". And anything that reads proposals as constraints — a person or an agent — must be able to tell whether one is still current.

**Implies.** The core does not enforce this; it says only that a merged proposal is the record. The rule, the reversal procedure and the validity check are `supersession`. A team without it decides case by case, and should adopt the pattern the first time the question comes up.

**Tension.** Immutability without a bridge to current-state documents produces an accurate ledger and a wrong README. `living-docs-bridge` is the bridge.

## P5. Single source for judgment — others link, never restate

**Statement.** The proposal is the source of truth for the intent and judgment behind its change — the problem's background, the alternatives rejected and why, the limits knowingly accepted. A document that needs this content links to the proposal; it does not restate it.

**Reasoning.** The same judgment written into two documents is edited apart and disagrees later, and every restatement is rewritten for its audience, so the copies drift by design, not by accident. Code already has this protection — C5 forbids the proposal to copy what code owns. The proposal's own content deserves the same rule in the other direction.

**Implies.** Whoever writes the PR description, the tracker comment or a state document decides its shape; when it needs the judgment recorded here, it points here. C5 and this principle are mirrors: the proposal does not duplicate what code, tests or the tracker own, and no document duplicates what the proposal owns.

**Tension.** A link is a click further than a paragraph, and a skimming reviewer may not follow it. A one-sentence summary next to the link is the accepted compromise; a full restatement is not.

---

## How the principles relate

P1 is about **cost**: documentation proportional to blast radius. P2 is about **truth**: judgment over description. P3, P4 and P5 are about **findability over time**: with the code, frozen, one source for the judgment.

When two conflict in a concrete case, truth wins over cost, and findability decides how (a linked appendix).
