# 샘플 읽기 안내

[English](README.md) | 한국어

가상의 개인 메모 앱을 소재로 두 Change Proposal 형식을 채워 쓴 예시입니다. 정식으로 유지하는 학습 자료이며, 이 저장소의 실제 구현 기록이나 승인된 제품 계획, 테스트 실행 증거는 아닙니다. 기본 언어는 영어이고 한국어판은 같은 이름의 `.ko.md` 파일로 제공합니다. 두 언어 모두 템플릿의 영어 섹션 이름과 동일한 요구사항·결정 ID를 유지합니다. 각 Split 문서 쌍은 같은 언어로 연결되며, 각 문서에서 다른 언어판으로 이동할 수 있습니다.

| 형식 | 샘플 | 이 형식이 적합한 이유 |
|---|---|---|
| Unified | [메모 검색어 한 번에 지우기](2026-09-12-clear-note-search.ko.md) | 기존 검색 흐름을 재사용하는 작은 UI 변경입니다. 의도·완료 기준·주요 선택을 한 문서에서 다룰 수 있습니다. |
| Split | 메모 휴지통과 30일 내 복원: [Product Requirements](2026-09-12-note-trash.requirements.ko.md) + [Technical Design](2026-09-12-note-trash.design.ko.md) | 사용자에게 약속하는 동작과 만료·복원 및 정리의 경쟁·접근 경계·데이터 전환을 분리해 검토할 필요가 있습니다. |

## 읽는 순서

1. Unified 샘플을 먼저 읽습니다. 여섯 섹션이 완전한 Proposal입니다. 변경이 짧아 선택적인 Summary를 생략했으며, 기술 설계 문서가 빠진 것이 아닙니다.
2. Split 샘플의 Product Requirements만 읽고 “이 동작이 필요한가, 범위와 약속이 적절한가?”를 판단합니다. 이어서 Technical Design을 읽고 “이 설계가 요구사항을 안전하게 충족하는가?”를 판단합니다.
3. 제품 문서의 R3에서 원래 메모를 복원한다는 약속을 확인하고, 기술 문서의 ID·내용 유지 선택과 Test Strategy의 검사 계획으로 따라가 봅니다. Verification에는 실제 구현 테스트를 실행하지 않았다고 명시되어 있습니다.

두 샘플은 서로 독립적인 변경이지, 순차적인 단계나 한 변경에 두 형식을 모두 작성하라는 요구가 아닙니다. 같은 가상 앱을 사용해 필요한 검토의 차이를 쉽게 비교할 수 있도록 했습니다. 형식은 문서 길이가 아니라 필요한 판단과 검토에 따라 선택합니다.

영어 기본판은 [메모 검색어 한 번에 지우기](2026-09-12-clear-note-search.md), [Product Requirements](2026-09-12-note-trash.requirements.md), [Technical Design](2026-09-12-note-trash.design.md)입니다. 번역은 같은 Proposal의 언어판이며 별도의 변경이 아닙니다. 예시의 동작·가정·결정을 바꾸면 두 언어를 함께 수정합니다.

이 페이지는 샘플 목록이며 Split Proposal의 세 번째 구성 문서가 아닙니다. 연결된 두 문서가 Proposal 전체입니다. 각 샘플은 가정을 명시하며, 실제 제안서는 가정을 조사한 저장소 근거로 대체하고 해당되는 경우 실제 검증 결과를 기록해야 합니다.

[기본 가이드](../docs/guide.md#choosing-a-form)에서 형식을 선택하고, [Split 가이드](../docs/split-proposals.md)에서 문서 쌍의 책임을 확인할 수 있습니다. 실제 변경을 작성할 때는 [Unified](../templates/change-proposal.md), [Product Requirements](../templates/product-requirements.md), [Technical Design](../templates/technical-design.md) 템플릿을 사용하고, 예시의 제품 정책을 그대로 기본값으로 삼지 마세요. 이 저장소의 실제 변경 기록은 [docs/changes](../docs/changes/)에 있습니다.
