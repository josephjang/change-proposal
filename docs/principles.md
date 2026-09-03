# Principles

Eleven principles. Each has a statement, the reasoning, what it implies, and the tension it creates. The core rules (`rules.md`) and every pattern cite them by number. When a rule and a principle conflict in a concrete case, the principle wins and the rule needs a proposal.

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

**Implies.** No schemas, payloads, file lists or work breakdowns in a proposal. Rejection reasons of the kind that would change if the facts changed. The four required core sections are all judgment.

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

## P5. Human authorship of judgment

**Statement.** The judgment in a proposal — framing, boundaries, decisions and their reasons, what is accepted — is written or explicitly confirmed by a person. An assistant may supply material and draft what can be derived from evidence.

**Reasoning.** The value of a proposal is the judgment it records. An assistant can generate plausible judgment-shaped text, which turns the absence of a decision into the appearance of one. Later, nobody can tell the difference.

**Implies.** The core says a person writes the proposal, and no more. The mechanics — which sections an assistant may draft, how drafts are marked, what agents are told — are `human-ai-split`.

**Tension.** The line between material and conclusion is not always crisp. When in doubt, the assistant asks.

## P6. Evidence, not claims

**Statement.** Verification records what was observed, not what was intended. What was not checked is stated as such.

**Reasoning.** "Tests pass" is a sentence anyone can write; a command and its output can only be written by someone who ran it. When text is cheap, this gap is the main integrity risk.

**Implies.** The `verification` pattern adds the section that asks for what was checked and observed and what was not. The stricter form — commands and results only, a mandatory "not done" entry, an agent rule — is `evidence-verification`.

**Tension.** Honest "not done" lists look like negligence to an unfamiliar reader. They are the opposite.

## P7. One vocabulary, progressive disclosure

**Statement.** Every section in every proposal, whatever patterns are on, uses a label from one fixed table. A larger proposal is a smaller one with sections added, never a different document.

**Reasoning.** A shared vocabulary is what makes patterns composable: each adds sections without colliding, and a proposal grows in place when a change turns out larger than expected.

**Implies.** Four required core labels plus the optional `Summary`; patterns add from the same table (`docs/patterns/README.md`). No pattern renames a section.

**Tension.** A fixed vocabulary resists local naming preferences. That is a deliberate constraint.

## P8. Ledger and state are different documents

**Statement.** Proposals are the ledger of transitions. Current-state documents — README, architecture notes, runbooks — are the state. The two are kept consistent by naming, at each transition, which state documents it touched.

**Reasoning.** A ledger alone makes "how does it work now" a reading of every entry; state alone loses "why". They connect only if each transition says what state it changed.

**Implies.** Nothing in the core. `living-docs-bridge` adds the section and the reviewer check.

**Tension.** A second place to keep honest. Teams that skip it get a precise ledger and a stale README.

## P9. Brevity by design

**Statement.** A proposal is one page. A section with nothing to say is deleted, not filled.

**Reasoning.** When drafting is free, the scarce resource is the reader's attention — a reviewer's, and an agent's context window. A long document with every section filled is not more complete; it is less read.

**Implies.** The core rule "one page, delete empty sections". Enforcement by tooling is `lint-gate`.

**Tension.** A page can be too small for a real decision. Reference an appendix or a link; do not exempt.

## P10. Start minimal, grow on signals

**Statement.** A team adopts the core alone and adds a pattern only when it meets the situation the pattern names. Nothing is adopted in anticipation.

**Reasoning.** Every pattern has a cost paid on every change and a benefit that appears only in the situation it was designed for. Adopting patterns up front pays all the costs and collects none of the benefits — until the practice is abandoned as ceremony.

**Implies.** Every pattern states its signal. A repository states its composition in `docs/changes/README.md`. Removing a pattern is as legitimate as adding one.

**Tension.** Signals are noticed in retrospect, after some pain. The pain of one missed review is smaller than the cost of a year of ceremony.

## P11. Single source for judgment — others link, never restate

**Statement.** The proposal is the source of truth for the judgment behind its change — the problem's background, the alternatives rejected and why, the limits knowingly accepted. A document that needs this content links to the proposal; it does not restate it.

**Reasoning.** The same judgment written into two documents is edited apart and disagrees later, and every restatement is rewritten for its audience, so the copies drift by design, not by accident. Code already has this protection — C5 forbids the proposal to copy what code owns. The proposal's own content deserves the same rule in the other direction.

**Implies.** Whoever writes the PR description, the tracker comment or a state document decides its shape; when it needs the judgment recorded here, it points here. C5 and this principle are mirrors: the proposal does not duplicate what code, tests or the tracker own, and no document duplicates what the proposal owns.

**Tension.** A link is a click further than a paragraph, and a skimming reviewer may not follow it. A one-sentence summary next to the link is the accepted compromise; a full restatement is not.

---

## How the principles relate

P1, P9 and P10 are about **cost**: proportional, brief, and only what is needed now. P2, P5 and P6 are about **truth**: judgment, honest authorship, honest verification. P3, P4, P7, P8 and P11 are about **findability over time**: with the code, frozen, one vocabulary, bridged to current state, one source for the judgment.

When two conflict in a concrete case — a long but truthful Verification against one page — truth wins over cost, and findability decides how (a linked appendix).
