# Q1 — Skill 제작 (`/bubu-report`)

## 무엇을 했는가

`skill-creator` 메타 스킬을 사용해 **부부 월간 결산 다이어리** 스킬(`bubu-report`)을 만들었습니다.
한 달간의 부부 일상을 의미 중심으로 정리해 `reports/YYYY-MM.md`에 저장하고,
인생작 후보와 부부 말버릇은 별도 누적 파일에 자동으로 쌓아둡니다.

## 어떻게 실행하는가

### 1. 준비물
- VS Code + Claude Code 확장
- 스킬 파일 (이 저장소에 포함): [.claude/skills/bubu-report/](../.claude/skills/bubu-report/)
  - `SKILL.md` — 트리거 · SOP · 7라운드 인터뷰 워크플로우
  - `assets/template.md` — 보고서 양식

### 2. 실행 방법
1. VS Code 재시작 또는 `Cmd+Shift+P → Reload Window`로 스킬 레지스트리 새로고침
2. 새 대화에서 다음 중 하나로 트리거:
   - 명시 호출: `/bubu-report`
   - 자연어: `"이번 달 결산 도와줘"`, `"결혼 10개월차 보고서 만들어줘"`, `"부부 일기 쓰자"`
3. 한 달치 메모를 자유롭게 던지고, AI가 묶음으로 던지는 인터뷰 질문에 답하기
4. 미리보기 확인 → 저장 → `reports/YYYY-MM.md` 생성

## 결과물 (스크린샷)

- `screenshot-trigger.png` — `/bubu-report` 트리거 화면
- `screenshot-interview.png` — 인터뷰 진행 화면
- `screenshot-result.png` — 저장된 `reports/2026-05.md` 예시
