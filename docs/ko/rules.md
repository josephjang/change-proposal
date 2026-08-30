# 규칙

> `docs/rules.md`의 한국어판. 어긋나면 영어판을 따른다. 규칙 ID와 키워드(MUST/SHOULD/MAY)는 영어 그대로 쓴다.

코어의 규범 부분. 여덟 개이며, 패턴을 하나도 도입하지 않은 팀에게 그 외에 요구되는 것은 없다. 각 패턴은 자기 규칙을 자기 카드(`docs/patterns/<name>.md`)에 담고, 저장소는 코어 규칙과 `docs/changes/README.md`에 적은 패턴의 규칙에 묶인다.

키워드는 RFC 2119를 따른다: **MUST** / **MUST NOT**은 요구사항, **SHOULD**는 이유를 적고 제안으로 뒤집을 수 있는 강한 기본값, **MAY**는 선택. 각 규칙은 섬기는 원칙(`principles.md`)을 인용한다.

구체적 상황에서 규칙과 원칙이 충돌하면 원칙이 이기고, 규칙에는 제안이 필요하다.

---

## 코어 규칙

| ID | 규칙 | 원칙 |
|---|---|---|
| **C1** | 관찰 가능한 동작을 바꾸는 변경은 제안을 가져야 한다(MUST). 바꾸지 않는 변경 — 동작이 같은 리팩터, 오타, 의존성 패치, 테스트만 — 은 제안을 가져서는 안 되며(MUST NOT), PR 설명에 동작 변화가 없다는 것과 어떻게 확인했는지를 적어야 한다(MUST). | P1, P3 |
| **C2** | 제안은 `docs/changes/YYYY-MM-DD-<slug>.md`에 있어야 하고(MUST), 변경과 같은 PR에 커밋되어야 한다(MUST). | P3 |
| **C3** | 제안은 제목과, 정확히 다음 레이블의 섹션을 이 순서로 가져야 한다(MUST): `Problem`, `Non-goals`, `Decisions`, `Verification`, `Risks & deferred`. 쓸 게 없는 섹션은 지워야 한다(MUST). 도입한 패턴이 더하는 섹션은 그 패턴이 정한 레이블을 쓴다. | P7, P9 |
| **C4** | 사람이 제안을 써야 한다(MUST). 재료는 어디서 와도 되지만, 각 섹션의 글은 사람의 판단이다. | P5 |
| **C5** | 제안은 코드·테스트·트래커가 정본인 내용 — 스키마, 시그니처, 페이로드, 파일 목록, 작업 분해 — 을 복제해서는 안 되며(MUST NOT), 참조해야 한다(MUST). | P2 |
| **C6** | `Non-goals`는 최소 한 항목을 이유와 함께 담아야 한다(MUST). | P2 |
| **C7** | `Decisions`는 대안이 있었던 결정만 담아야 한다(MUST). 각 항목은 무엇을 골랐고, 무엇을 버렸고, 사실이 바뀌면 결론도 바뀌는 종류의 이유를 적어야 하며(MUST), 재검토 조건을 적는 것이 좋다(SHOULD). | P2 |
| **C8** | `Verification`은 무엇을 확인하고 무엇을 관찰했는지 적어야 하고(MUST), 무엇을 확인하지 않았는지와 이유를 적어야 한다(MUST). 제안은 한 장에 들어가는 것이 좋다(SHOULD). | P6, P9 |

---

## 코어 규칙이 말하지 않는 것

자주 나오는 질문 중 답이 코어 규칙이 아니라 패턴인 것들. 해당 패턴을 도입하지 않은 팀에는 그 문제에 대한 규칙이 없고, 사례별로 정한다.

| 질문 | 패턴 |
|---|---|
| 이 변경은 코드를 쓰기 전에 리뷰가 필요한가? | `risk-signals`, `design-first-review` |
| 티어나 크기 라벨이 있는가? | `sizing-tiers` |
| 머지된 제안을 고쳐도 되는가? 어떻게 뒤집는가? | `supersession` |
| front matter — 담당자, 상태, 링크, 태그 — 가 있는가? | `proposal-metadata` |
| 제안이 "끝났다"를 정의해야 하는가? | `success-criteria` |
| 무엇이 바뀌었는지 기술해야 하는가? | `before-after` |
| AI가 일부를 초안해도 되는가, 어떻게 표시하는가? | `human-ai-split` |
| 검증은 명령과 출력이어야 하는가? | `evidence-verification` |
| 낡게 만든 문서를 나열해야 하는가? | `living-docs-bridge` |
| 표준은 어디로 가는가? | `decision-promotion` |
| 몇 주짜리 일은 어떻게 조직하는가? | `initiative-umbrella` |
| 결과를 다시 보는가? | `outcome-review` |
| 에이전트가 제안을 읽는가? 스킬이 있는가? | `agent-context`, `agent-skills` |
| CI가 무언가를 검사하는가? | `lint-gate` |
| 제안을 다른 언어로 써도 되는가? | `multilingual-records` |
