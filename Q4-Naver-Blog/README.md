# Q4 — Naver Blog 초안 자동화 (`/naver-blog`)

## 무엇을 했는가

기사·웹페이지 **URL 하나만 주면** 네이버 블로그용 초안을 자동으로 만들어주는 스킬을 제작했습니다.

- 스킬 이름: **`naver-blog`**
- 스킬 정의: [.claude/skills/naver-blog/SKILL.md](../.claude/skills/naver-blog/SKILL.md)
- 도구 조합: **WebFetch**(기사 본문 수집) + **Playwright MCP**(네이버 로그인 → 작성창 → 임시저장)

기사를 친구한테 카톡 풀어주듯 캐주얼한 톤(반말 + "핵심만 말하면" 말버릇)으로 **도입 / 핵심 내용 / 내 생각 / 마무리** 4단 구조로 정리합니다. 발행은 절대 자동으로 누르지 않고 **임시저장까지만** 진행합니다.

## 어떻게 실행하는가

### 1. 준비물
- VS Code + Claude Code 확장
- [.mcp.json](../.mcp.json)에 등록된 `@playwright/mcp` (이 저장소에 포함)
- 네이버 자격증명: `.env` 파일에 `NAVER_ID`, `NAVER_PW` 설정
  - 양식: [.env.example](.env.example)
  - `.env`는 [.gitignore](../.gitignore)에 등록돼 절대 GitHub에 올라가지 않음

### 2. 실행 방법
1. VS Code 재시작 또는 `Cmd+Shift+P → Reload Window`로 스킬 레지스트리 새로고침
2. 새 대화에서 다음 중 하나로 트리거:
   - 명시 호출: `/naver-blog https://example.com/article/123`
   - 자연어: `"이 기사 블로그 초안 써줘: <URL>"`, `"이 URL 네이버 블로그용으로 정리"`
3. AI가 URL 분석 → 4단 초안 작성 → `Q4-Naver-Blog/draft.md`에 저장
4. (선택) Playwright MCP로 네이버 로그인 시도 → 작성창에 붙여넣기 → **임시저장 버튼 클릭**
5. 사용자는 네이버 블로그에서 직접 검토 후 발행

> ⚠️ **CAPTCHA 대응**: 네이버 로그인이 자동입력방지 문자로 막히면 스킬이 즉시 중단되고, `draft.md`만 저장한 상태로 사용자에게 핸드오프됩니다. 수동으로 로그인 후 본문을 직접 붙여넣으면 됩니다.

## 결과물

| 파일 | 내용 |
|------|------|
| [draft.md](draft.md) | 실제 생성된 초안 — "대학가에 번지는 'AI 디바이드'" 기사 |
| [.env.example](.env.example) | 자격증명 양식 (실제 `.env`는 깃에 안 올라감) |
| [screenshot-result.png](screenshot-result.png) | 네이버 블로그 임시저장 결과 (또는 초안 미리보기) |

### 원본 기사
[newsis — "유료 구독이 성적 가른다"…대학가 번지는 'AI 디바이드'](https://www.newsis.com/view/NISX20260520_0003637590)

## 설계 포인트

- **톤은 SKILL.md에 박제.** 다음 대화에서도 같은 친구체 + "핵심만 말하면" 말버릇이 자동으로 재현됨.
- **사실/의견 분리.** 숫자·고유명사는 원문 그대로, 추측은 "내 생각" 섹션에만.
- **발행은 사람 손으로.** 스킬은 임시저장까지만. 자동 발행은 절대 안 함.
- **CAPTCHA·2차 인증 등 차단 발생 시 즉시 중단** → `draft.md`만 남기고 사용자에게 핸드오프.
