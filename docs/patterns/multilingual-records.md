# Pattern: multilingual-records

- **Requires**: core
- **Combines with**: `proposal-metadata` (front matter stays English), `agent-context` (agents search by English labels and tags whatever the body language), `lint-gate` (heading resolution is checked), `human-ai-split` (assistants do not translate a person's text)
- **Conflicts with**: —

## Intent

Let a team write proposals in its own language while everything a machine or a cross-team reader relies on — section labels, front matter, tags, file names — stays English.

## Signal

The team writes, or wants to write, proposals in a language other than English; or a repository is shared between teams writing in different languages.

## Adds

**A record language**, declared once in `docs/changes/README.md` (`Record language: ko`).

**A heading rule.** A non-English heading carries the English label in parentheses after the local label:

```
## 문제 (Problem)
## 결정과 기각한 대안 (Decisions)
## 검증 (Verification)
```

English headings carry nothing extra. Readers use the local label; tooling and agents use the parenthesis.

**A label table** for the language — the local name for each label in `docs/patterns/README.md`. Korean is provided:

| Label | Korean |
|---|---|
| Problem | 문제 |
| Non-goals | 비목표 |
| Goals / Non-goals | 목표 / 비목표 |
| Decisions | 결정과 기각한 대안 |
| Verification | 검증 |
| Risks & deferred | 감수한 리스크와 미룬 것 |
| Success criteria | 완료 기준 · 성공 지표 |
| Change | 변경 |
| Summary | 요약 |
| Rollout & rollback | 롤아웃과 롤백 |
| Cross-cutting concerns | 횡단 관심사 |
| Open questions | 열린 질문 |
| Living docs | 살아있는 문서 |
| Current structure · Design · Milestones | 현재 구조 · 설계 · 마일스톤 |
| Outcome | 결과 |

**Four invariants**, regardless of body language: front-matter keys and values, `status`, file names and slugs, `touches` tags are English.

**A translation rule**: merged proposals are never translated — a translation would be a second, unfrozen copy. The practice's own documents are authored in English with translations that follow; where they disagree, the English text is authoritative.

**A template** in the record language (`templates/ko/change-proposal.md` for Korean).

## Rules

| ID | Rule | Principle |
|---|---|---|
| **ML1** | The record language MUST be declared in the composition. | P7 |
| **ML2** | Front-matter keys and values, `status`, file names, and `touches` MUST be English regardless of the record language. | P7 |
| **ML3** | A heading in a non-English proposal MUST carry the English label in parentheses after the local label. English headings carry nothing extra. | P7 |
| **ML4** | A merged proposal MUST NOT be translated. Translations of the practice's own documents MUST follow the English text. | P4 |
| **ML5** | An assistant MUST draft in the record language and MUST NOT translate a person's text. | P5 |

## Cost

A parenthesis per heading in non-English proposals. Translations of the practice's documents cost effort to keep current; "English wins" keeps that from becoming a correctness problem.

## Remove

Set the record language to English. Existing non-English proposals remain valid — the heading rule already made them machine-readable.
