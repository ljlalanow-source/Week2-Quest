# Q2 — Subagent (팩트체크 파이프라인)

## 선택한 주제
**E. 불확실한 정보 → 찾고 검증해서 최종 결론 제시**

모호한 주장 하나를 받아 → 자료 수집 → 교차 검증 → 신뢰도 등급 포함 결론으로 정리하는 3단 파이프라인.

## 에이전트 구성

| # | 이름 | 역할 | 입력 | 출력 |
|---|------|------|------|------|
| 1 | **fact-finder** | 자료 수집 | 검증할 주장 한 문장 | 출처 3~5개 + 핵심 인용문 |
| 2 | **cross-verifier** | 교차 검증 | fact-finder의 출처 모음 | 일치/모순 분석 + 신뢰도 등급(A~D) |
| 3 | **conclusion-writer** | 최종 판정 | 위 두 결과 | ✅/⚠️/❌/❓ 판정 + 근거 3줄 + 출처 |

각 에이전트 정의는 [.claude/agents/](../.claude/agents/) 폴더에 저장됨:
- [fact-finder.md](../.claude/agents/fact-finder.md)
- [cross-verifier.md](../.claude/agents/cross-verifier.md)
- [conclusion-writer.md](../.claude/agents/conclusion-writer.md)

전체 팀 설계 문서: [team.md](team.md)

## 핸드오프 흐름

```
사용자 질문
   │
   ▼
[fact-finder]  → 출처 + 인용 묶음
   │
   ▼
[cross-verifier] → 일치/모순 + 신뢰도 평가
   │
   ▼
[conclusion-writer] → 최종 판정 + 근거 요약
```

## 실제 실행 결과

**검증 주장:** "한국에서 결혼 1주년 선물로 '종이(paper)'를 주는 것이 전통이다."

**판정:** ⚠️ 부분 사실 (신뢰도 4/5)

> 종이 선물 풍습은 한국 고유 전통이 아니라 19세기 서양에서 시작된 관습이 한국에 수용된 것. "전통"의 정의에 따라 판정이 갈려서 ⚠️로 판정.

전체 결과 마크다운: [factcheck-result.md](factcheck-result.md)

## 호출 방법

새 Claude Code 세션에서 다음과 같이 호출:

```
@fact-finder "검증할 주장 한 문장"
```

또는 그냥 자연어로 — Claude가 description을 읽고 자동으로 적절한 에이전트를 호출함:

```
이 주장이 사실인지 확인해줘: "..."
```

3단계가 순서대로 실행되도록 메인 Claude에게 다음처럼 요청:

```
@fact-finder로 조사 → @cross-verifier로 검증 → @conclusion-writer로 정리, 순서대로 진행해줘.
주장: "..."
```

## 설계 포인트

- **단방향 파이프라인.** 각 에이전트는 앞 단계 결과만 받음 → 메인 컨텍스트 절약.
- **역할 분리.** 조사관은 판정 안 함, 검증관은 결론 안 냄. 마지막 작성관만 ✅/⚠️/❌/❓를 결정.
- **불확실하면 ❓.** 출처 부족·모순 클 때 억지로 결론 내리지 않도록 명시.

## 스크린샷
![서브에이전트 실행 결과](screenshot-result.png)

> 참고: 위 [factcheck-result.md](factcheck-result.md) 파일이 실제 에이전트 파이프라인이 만들어낸 출력. 스크린샷은 Claude Code에서 같은 워크플로우를 실행했을 때의 채팅 화면.
