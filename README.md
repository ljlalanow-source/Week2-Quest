# Week 2 Quest — Claude Code 실전 자동화

2주차 핵심 도구(**스킬 · 서브에이전트 · MCP**)를 실제 업무에 적용해 만든 자동화 결과물 모음입니다.

## 전체 구조

```
Week2-Quest/
├── .gitignore
├── .claude/                  # 스킬 & 에이전트 정의
│   ├── skills/
│   │   ├── meeting-summary/  # Q1: 회의록 → 요약 + 액션 아이템
│   │   ├── yt-summary/       # Q3: YouTube URL → 자막 요약
│   │   ├── naver-blog/       # Q4: 기사 URL → 네이버 블로그 초안
│   │   └── news-card/        # Q5: 기사 URL → 인스타 뉴스 카드
│   └── agents/
│       ├── researcher.md     # Q2: 경쟁사·시장 조사
│       ├── analyst.md        # Q2: 비교/인사이트 추출
│       └── writer.md         # Q2: 최종 보고서 작성
├── Q0-GWS-CLI/    # 구글 워크스페이스 CLI 활용
├── Q1-Skill/      # skill-creator로 직접 만든 스킬
├── Q2-Subagent/   # 멀티 에이전트 팀 구성
├── Q3-YT-Summary/ # yt-dlp + Claude 요약 스킬
├── Q4-Naver-Blog/ # Playwright MCP로 블로그 초안 자동화
└── Q5-News-Card/  # 기사 → 인스타 뉴스 카드(HTML/PNG)
```

## 퀘스트 요약

| # | 주제 | 핵심 도구 |
|---|------|-----------|
| Q0 | 구글 워크스페이스 CLI로 메일/캘린더 자동화 | GWS CLI |
| Q1 | skill-creator로 회의록 요약 스킬 제작 | Skill |
| Q2 | researcher/analyst/writer 3-에이전트 협업 | Subagent |
| Q3 | YouTube 영상 → 자막 요약 스킬 | yt-dlp + Skill |
| Q4 | 기사 URL → 네이버 블로그 초안 임시저장 | Playwright MCP |
| Q5 | 기사 URL → 인스타용 뉴스 카드 HTML/PNG | HTML + 스킬 |

## 사용 방법

각 퀘스트 폴더의 `README.md`에 실행 방법과 결과 스크린샷이 정리돼 있습니다.

모든 스킬과 에이전트는 `.claude/` 디렉터리에 정의돼 있고, Claude Code에서 자동으로 인식됩니다. 새 대화에서 `/[스킬명]` 또는 서브에이전트 호출(`@[에이전트명]`)로 사용할 수 있습니다.

## 보안 / 비밀 정보

- `.env` 파일은 `.gitignore`에 등록돼 GitHub에 올라가지 않습니다.
- 네이버 ID/PW 등은 `Q4-Naver-Blog/.env.example` 양식을 참고해 본인이 직접 `.env`로 만들어 사용하세요.
