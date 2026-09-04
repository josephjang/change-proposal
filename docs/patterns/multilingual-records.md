# Pattern: multilingual-records

Lets a team write proposals in its own language while everything a machine or a cross-team reader relies on, section names, front matter, tags, file names, stays English.

**When.** The team writes, or wants to write, proposals in a language other than English; or a repository is shared between teams writing in different languages.

**Goes with.** `proposal-metadata` (front matter stays English), `agent-context` (agents search by English names and tags whatever the body language), `lint-gate` (heading resolution is checked), `human-ai-split` (assistants do not translate a person's text).

## What it adds

**A record language**, declared once in `docs/changes/README.md` (`Record language: ko`).

**A heading convention.** A non-English heading carries the English section name in parentheses after the local one:

```
## 문제 (Problem)
## 결정과 기각한 대안 (Decisions)
## 검증 (Verification)
```

English headings carry nothing extra. Readers use the local name; tooling and agents use the parenthesis.

**A table of local names** for the section headings. Korean is provided here; another language adds its own column.

| Section | Korean |
|---|---|
| Problem | 문제 |
| Non-Goals | 비목표 |
| Goals | 목표 |
| Decisions | 결정과 기각한 대안 |
| Product Decisions | 제품 결정 |
| Technical Decisions | 기술 결정 |
| Verification | 검증 |
| Risks | 리스크 |
| Requirements | 요구사항 |
| Change | 변경 |
| Summary | 요약 |
| Rollout & rollback | 롤아웃과 롤백 |
| Cross-cutting concerns | 횡단 관심사 |
| Open questions | 열린 질문 |
| Living docs | 살아있는 문서 |
| Current structure · Design · Milestones | 현재 구조 · 설계 · 마일스톤 |
| Outcome | 결과 |

**A template** in the record language, created by the adopter from the shipped one.

## Using it

- Regardless of body language, four things stay English: front-matter keys and values, `status`, file names and slugs, `touches` tags.
- A merged proposal is never translated. A translation would be a second, unfrozen copy of a record.
- An assistant drafts in the record language and does not translate a person's text.

## Cost

A parenthesis per heading in non-English proposals.

## Removing it

Set the record language to English. Existing non-English proposals remain valid; the heading convention already made them machine-readable.
