# Week 2 Quest — Claude Code 실전 자동화

2주차 핵심 도구(**스킬 · 서브에이전트 · MCP**)를 실제 업무에 적용해 만든 자동화 결과물 모음입니다.

## 전체 구조

```
Week2-Quest/
├── .gitignore
├── .mcp.json                 # Playwright MCP 등록
├── .claude/                  # 스킬 & 에이전트 정의
│   ├── skills/
│   │   ├── skill-creator/    # 메타 스킬 (새 스킬 제작용)
│   │   ├── bubu-report/      # Q1: 부부 월간 결산 다이어리
│   │   ├── naver-blog/       # Q4: 기사 URL → 네이버 블로그 초안
│   │   └── news-card/        # Q5: 기사 URL → 인스타 뉴스 카드
│   └── agents/
│       ├── fact-finder.md    # Q2: 자료 수집 (출처 3~5개)
│       ├── cross-verifier.md # Q2: 교차 검증 + 신뢰도 등급
│       └── conclusion-writer.md # Q2: 최종 판정 + 근거 요약
├── Q0-GWS-CLI/    # 구글 워크스페이스 CLI 활용 (미진행)
├── Q1-Skill/      # skill-creator로 bubu-report 스킬 제작
├── Q2-Subagent/   # 팩트체크 3-에이전트 파이프라인
├── Q3-YT-Summary/ # yt-dlp + Python + Claude 유튜브 요약
├── Q4-Naver-Blog/ # Playwright MCP로 블로그 초안 자동화
├── Q5-News-Card/  # 기사 → 인스타 뉴스 카드(HTML/PNG)
└── reports/       # bubu-report 스킬이 저장하는 월간 결산
```

## 퀘스트 요약

| # | 주제 | 핵심 도구 | 상태 |
|---|------|-----------|------|
| Q0 | 구글 워크스페이스 CLI로 메일/캘린더 자동화 | GWS CLI | ⏳ 미진행 |
| Q1 | skill-creator로 부부 월간 결산 다이어리 스킬(`/bubu-report`) 제작 | Skill | ✅ |
| Q2 | fact-finder → cross-verifier → conclusion-writer 팩트체크 파이프라인 | Subagent | ✅ |
| Q3 | yt-dlp로 자막 수집 → Python 정리 → Claude 구조화 요약 | yt-dlp + Skill | ✅ |
| Q4 | 기사 URL → 네이버 블로그 초안 임시저장(`/naver-blog`) | Playwright MCP | ✅ |
| Q5 | 기사 URL → 인스타용 뉴스 카드 HTML/PNG(`/news-card`) | HTML + 스킬 | ✅ |

## 사용 방법

각 퀘스트 폴더의 `README.md`에 실행 방법과 결과 스크린샷이 정리돼 있습니다.

모든 스킬과 에이전트는 `.claude/` 디렉터리에 정의돼 있고, Claude Code에서 자동으로 인식됩니다. 새 대화에서 `/[스킬명]` 또는 서브에이전트 자연어 호출로 사용할 수 있습니다.

## 보안 / 비밀 정보

- `.env` 파일은 `.gitignore`에 등록돼 GitHub에 올라가지 않습니다.
- 네이버 ID/PW 등은 `Q4-Naver-Blog/.env.example` 양식을 참고해 본인이 직접 `.env`로 만들어 사용하세요.
