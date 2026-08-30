# 패턴

> `docs/patterns/README.md`의 한국어판. 어긋나면 영어판을 따른다. 각 패턴 카드(`docs/patterns/<name>.md`)는 영어만 있다.

코어(`concept.md`, `rules.md`)는 완결되어 있고 작다. 팀이 그 너머에서 원할 수 있는 모든 것은 **패턴**이다: 독립적으로 도입·조정·제거할 수 있는 선택적 추가. 이 카탈로그는 패턴을 나열하고, 조합 방법을 말하고, 조합 예시를 준다.

## 패턴이란

모든 패턴 카드는 같은 부분으로 되어 있다.

- **의도** — 해결하는 문제 하나.
- **신호** — 도입할 때가 되었음을 알려 주는 관찰 가능한 상황. 신호 없는 패턴은 의식(ceremony)이다(P10); 여기에는 없다.
- **더하는 것** — 섹션(레이블 포함), front matter 필드, 단계, 문서, 도구 요구사항. 섹션 본문이 카드에 있으므로 카드만으로 충분하다.
- **규칙** — 패턴 자체의 규칙. ID가 있고 코어와 같은 MUST/SHOULD/MAY 형식.
- **요구 / 조합 / 충돌**.
- **비용** — 패턴이 켜져 있는 동안 모든 변경이 치르는 것.
- **제거** — 방법과, 그 아래 쓰인 제안이 어떻게 되는지(거의 항상: 그대로 유효).

## 카탈로그

| 패턴 | 의도 | 신호 | 더하는 것 |
|---|---|---|---|
| `risk-signals` | 계약·비가역·민감 영역 변경에 코드 전 리뷰와 롤아웃 블록 | 만들기 전에 논의했으면 했던 첫 변경 | 세 질문; `Rollout & rollback`, `Cross-cutting concerns`; 코드 전 리뷰어 |
| `proposal-metadata` | front matter: 담당자, 상태, 링크, 태그 | 날짜 외의 기준으로 제안을 찾아야 하거나, 변경이 PR 여러 개에 걸침 | front matter 블록과 필드; `status` |
| `supersession` | 머지된 제안은 불변, 새 제안으로 뒤집음 | 누군가 머지된 제안을 "고치고" 싶어 함 | `supersedes` / `superseded_by`; 뒤집는 절차 |
| `human-ai-split` | AI는 도출 가능한 것을 초안, 사람은 판단, 초안은 표시 | 제안 작성에 AI를 씀 | 섹션 분류; `<!-- ai-draft -->` 마커; AI 지침 |
| `evidence-verification` | 검증은 명령과 관찰만 | AI가 구현하거나 테스트함 | 엄격한 섹션 형태; 리뷰어 테스트; 에이전트 규칙 |
| `success-criteria` | 참/거짓으로 판정하는 "끝났다"의 정의 | "끝났나?"가 논쟁이 되거나, 다른 사람이 제안대로 구현함 | `Goals / Non-goals`(`Non-goals`를 대체), `Success criteria` |
| `before-after` | diff를 열지 않을 독자에게 무엇이 바뀌었는지 | 제안을 몇 달 뒤나 에이전트가 읽는데 변경을 재구성할 수 없음 | `Change` (전 / 후 / 어디) |
| `sizing-tiers` | 루브릭으로 정하는 명시적 T0–T3 티어 | 얼마나 리뷰했어야 했나에 대한 사후 논쟁 반복 | `tier` 필드; 루브릭; 티어별 상한 |
| `design-first-review` | 문서만 담은 PR이 구현 전 `accepted`에 도달 | 위험한 변경이 완성된 코드로 도착해 리뷰어가 되돌릴 수 없음 | `accepted` 상태; `Open questions`; 2단계 흐름 |
| `spike-then-spec` | 만들어 보고 배운 뒤 제안을 씀 | 이미 있는 프로토타입을 정당화하려고 제안을 씀 | 규칙 셋; `abandoned` 상태 |
| `living-docs-bridge` | 위험한 변경마다 갱신한 현재-상태 문서를 적음 | "지금 어떻게 동작해?"에 제안 여러 장이 필요 | `Living docs` |
| `decision-promotion` | 변경보다 오래 사는 결정을 결정 기록으로 | 같은 결정이 세 곳 이상에서 인용됨 | `docs/decisions/`; 기록 템플릿 |
| `initiative-umbrella` | 다주 작업을 위한 브리프 + 설계 + 하위 제안 | 한 달 넘는 다팀 이니셔티브 시작 | 이니셔티브 디렉터리; 브리프·설계 문서; `parent` |
| `outcome-review` | 출시 후 선언한 지표를 실제와 비교 | 지표를 선언하고 다시 보지 않음 | `outcome.md`; 일정 |
| `agent-context` | 코딩 에이전트가 머지된 제안을 제약으로 읽음 | 에이전트가 기각한 대안을 다시 만들거나 비목표를 함 | 에이전트 지침 블록; `touches` 어휘 |
| `agent-skills` | Claude Code·Codex용 스킬로 기계적 부분을 처리 | 같은 지시를 세션마다 붙여 넣음 | 스킬 명세(각각 무엇을 해야 하는가) |
| `lint-gate` | CI가 기계적 규칙을 집행 | 마커가 남은 채 머지, 또는 제안 없이 동작 변경 머지 | 린트 명세; 집행 수준 |
| `multilingual-records` | 영어가 아닌 제안도 기계가 읽을 수 있게 | 팀이 둘 이상의 언어로 씀 | 제목 규칙; 불변 조건 |

## 섹션 레이블

코어와 모든 패턴이 쓰는 하나의 표. 어떤 패턴도 섹션 이름을 바꾸지 않는다; 제안은 이 표의 행을 더해 자란다.

| 레이블 | 도입 | 대체 |
|---|---|---|
| `Problem` | 코어 | |
| `Non-goals` | 코어 | |
| `Decisions` | 코어 | |
| `Verification` | 코어 | |
| `Risks & deferred` | 코어 | |
| `Goals / Non-goals` | `success-criteria` | `Non-goals` |
| `Success criteria` | `success-criteria` | |
| `Change` | `before-after` | |
| `Summary` | `sizing-tiers` (T2+), `initiative-umbrella` | |
| `Rollout & rollback` | `risk-signals` | |
| `Cross-cutting concerns` | `risk-signals` | |
| `Open questions` | `design-first-review` | |
| `Living docs` | `living-docs-bridge` | |
| `Current structure`, `Design`, `Milestones` | `initiative-umbrella` (브리프·설계 문서에서만) | |
| `Outcome` | `outcome-review` | |

한국어 레이블은 `multilingual-records` 패턴 카드에 있다.

## 조합

1. **코어는 항상 켜져 있다.** 모든 패턴이 코어를 요구한다.
2. **패턴은 덧셈이다.** 각 패턴은 섹션·필드·단계·규칙을 더하고 다른 패턴의 것을 다시 쓰지 않는다. 공유 레이블 표(P7)가 이를 보장한다.
3. **요구사항은 카드에 선언된다.** 대부분은 코어만 요구한다. 일부는 다른 패턴을 요구한다(예: `supersession`은 `status` 필드를 위해 `proposal-metadata`를, `design-first-review`는 어느 제안에 단계가 필요한지 알기 위해 `risk-signals`나 `sizing-tiers`를).
4. **충돌은 선언되지, 발견되지 않는다.** 하나 있다: 머지된 제안을 제자리에서 고치는 것(`supersession` 없음)은 `agent-context`와 양립하지 않는다 — 에이전트가 어느 제안이 최신인지 알 수 없다.
5. **저장소의 규칙은 코어 규칙 + 도입한 패턴의 규칙이다.** 그 외에는 아무것도 묶지 않는다.
6. **제거는 정당하다.** 각 카드가 방법을 적는다. 제거된 패턴 아래 쓰인 제안은 그대로 남는다.
7. **매개변수는 도입하는 쪽의 것이다.** 패턴에 손잡이(단어 상한, 리뷰어 수, 리뷰 SLA)가 있으면 카드가 이름과 기본값을 주고, 값은 저장소의 `docs/changes/README.md`에 적는다.

## 조합 선언

저장소는 `docs/changes/README.md` 맨 위에 산문으로 조합을 적는다:

> 이 저장소는 change-proposal 코어에 `risk-signals`, `human-ai-split`, `evidence-verification`을 더해 쓴다. 위험 신호 시 리뷰어: 1명. 단어 상한: 한 장.

이것이 기제의 전부다. 도구를 가져오는 패턴(`lint-gate`, `agent-skills`)은 같은 문장을 설정 파일로 형식화할 수 있다; 사람에게는 산문이 정본이다.

## 조합 예시

출발점이지 처방이 아니다. 각각 코어에 나열한 패턴을 더한 것이다.

| 상황 | 패턴 | 비고 |
|---|---|---|
| 한 사람 또는 아주 작은 팀, AI를 매일 씀 | `risk-signals`, `human-ai-split`, `evidence-verification` | AI 초안을 정직하게 유지하는 가장 작은 조합 |
| 공유 계약이 몇 개 있는 제품 팀 | + `proposal-metadata`, `supersession`, `agent-context`, `living-docs-bridge`, `spike-then-spec` | 머지된 제안이 에이전트 제약이 되고, 상태 문서가 정직해진다 |
| 계약이 산출물인 플랫폼 팀 | + `sizing-tiers`, `design-first-review`, `decision-promotion`, `lint-gate` | 코드 전 리뷰가 강제 가능해지고, 표준에 집이 생긴다 |
| 분기 이니셔티브를 돌리는 여러 팀 | + `initiative-umbrella`, `outcome-review`, `success-criteria` | 제안 하나보다 큰 일, 결과를 다시 본다 |
| 위 어느 것이든, 한국어로 | + `multilingual-records` | 제목에 영문 레이블; 기계가 읽는 부분은 영어 |

조합 간 이동은 `docs/changes/README.md`의 줄을 더하거나 빼는 것이다. 이미 쓰인 것은 바뀌지 않는다.

## 새 패턴 제안하기

새 패턴은 이 저장소의 변경이며 제안으로 도착한다(`CONTRIBUTING.md`). 신호 — 기존 패턴이 다루지 못한 실제 상황 — 와 변경당 비용을 보여야 하고, 위 표의 레이블을 쓰거나 표가 커져야 하는 이유를 설명해야 한다. 신호를 말할 수 없는 패턴은 거절된다.
