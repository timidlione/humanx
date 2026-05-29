# HumanX — 세션 핸드오프 (v0.5 final → Phase 2 진입 직전)

> 이전 세션의 작업 요약. `CLAUDE.md` (507줄 명세 v3)와 함께 읽을 것.
> 사용자는 `/clear` 후 이 문서로 다음 세션을 시작합니다.

---

## 🎯 현재 상태

**MVP 0.5 final** — Phase 1 프론트엔드 100% 완성. Phase 2 백엔드 진입 직전.
- 4개 정적 HTML 페이지 (`index` · `modules` · `simulation` · `benchmark`)
- 12개 인터랙티브 모듈 (CAT 01·02·03·04 + Phase 3 미리보기 06·07)
- CLAUDE.md v3 명세 완전 정렬
- 사용자 피드백 21건 누적 반영

**GitHub:** https://github.com/timidlione/humanx
**배포:** https://timidlione.github.io/humanx/
**Working dir:** `/Users/siong/Desktop/HumanX`

---

## 📁 파일 구조

```
HumanX/
├── CLAUDE.md       명세 v3 (507줄) — 1~9장 + 부록 A·B·C
├── CLAUDE2.md      이 문서 (세션 핸드오프)
├── README.md       프로젝트 개요 + 12 모듈 표 + 시스템 + Phase 2 체크리스트
├── index.html      랜딩 — WebGL 파티클 뇌 · 자극적 ticker · 6축 mini radar · OG 메타
├── modules.html    12 카드 카탈로그 — CAT 번호 + Phase 배지 + 동작 필터 + SVG 일러스트
├── simulation.html 12 모듈 인터랙티브 — 좌(체류/진행/권장) 중(문제) 우(⚔ AI 대결 + 채점 + 사고 흔적)
└── benchmark.html  진척도 → 점수 산출 → AA Index → 6축 + Turing → 모델 매칭 → 리더보드 → 개방형 3단 → 공유
```

**localStorage 키:**
- `humanx:last-result` — 가장 최근 모듈 결과 (벤치마크가 읽음)
- `humanx:history` — 누적 결과 배열 (같은 모듈은 최신으로 갱신, 최대 30개)

---

## 📚 12개 모듈

| 코드 | 제목 | CAT | Type | 채점 | 단축 |
| --- | --- | --- | --- | --- | --- |
| F-01 | 삼단논법 — 타당성/건전성 | 01 Foundation | MCQ × 5 가중치 | 정답형 | `?mod=F-01` |
| F-02 | 베이지안 갱신 | 01 Foundation | MCQ × 3 가중치 | 정답형 | `?mod=F-02` |
| F-03 | 비공식 오류 감별 | 01 Foundation | Flag (F1) | 정답형 | `?mod=F-03` |
| M-01 | 8개 공과 양팔 저울 | 02 Cognition | Open + 체크포인트 | 개방형 | `?mod=M-01` |
| M-02 | 두 밧줄로 45분 | 02 Cognition | Open + 체크포인트 | 개방형 | `?mod=M-02` |
| M-03 | 스쿨버스 골프공 Fermi | 02 Cognition | Open + 체크포인트 | 개방형 | `?mod=M-03` |
| E-01 | divide() Edge Case | 03 Engineering | MCQ × 4 가중치 | 정답형 | `?mod=E-01` |
| E-02 | 반복 중 리스트 수정 | 03 Engineering | MCQ × 3 가중치 | 정답형 | `?mod=E-02` |
| E-03 | URL 단축 서비스 역설계 | 03 Engineering | Open + 체크포인트 | 개방형 | `?mod=E-03` |
| C-02 | 새벽 3시 다중 장애 | 04 Crisis | Open + 체크포인트 | 개방형 | `?mod=C-02` |
| H-01 | AI 환각 감별 (양자 의료) | 06 Phase 3 Preview | Flag (F1) | 정답형 | `?mod=H-01` |
| R-03 | 원격 근무 적대적 토론 | 07 Phase 3 Preview | Open + 체크포인트 | 개방형 | `?mod=R-03` |

---

## ⚙ 핵심 시스템 (명세 v3 정렬)

### 두 갈래 채점 (CLAUDE.md 2.2)
- **정답형:** F-01·F-02·F-03·E-01·E-02·H-01 — 키워드/공식 매칭 → "정답입니다 ✓ / 틀렸습니다 ✗" + 해설
- **개방형:** M-01·M-02·M-03·E-03·C-02·R-03 — "맞다/틀리다" 판정 **금지**. ① 사용자 접근 **인정** → ② 다룬 **체크포인트** 표시 → ③ **대안** 사고 경로 제시
- 각 open 모듈 데이터에 `checkpoints: [{label, desc}]` + `alternatives: [...]` 필드 보유

### AI 모델 매칭 (CLAUDE.md 2.3)
- "당신 ≈ Gemini 3.5 Flash · AA 55 / 60" 직접 매칭 카드 (benchmark 히어로)
- 525 LLM 리더보드 (현재 60개 발췌, 코드 `LEADERBOARD` 배열)
- 점수대별 정성 설명 (최신 프런티어 / 중상위권 / 중위권 / 경량 상위 / 경량)
- ⚠ 명세 주의: 모델 목록·점수를 코드에 하드코딩하지 말 것 → Phase 2에서 config/DB 분리 필요

### AI 풀이 시간 (CLAUDE.md 4.2)
- `AI_BENCH` (simulation.html) — 12 모듈 × 3 모델 (GPT-5.5 / Opus 4.7 / 7B 경량)
- simulation 우측 "⚔ AI 대결" 패널 + benchmark "당신 vs AI" 비교

### 6축 레이더 (CLAUDE.md 4.3)
- 공감 · 유연 · 다중 맥락 · 은유·직관 · **창의적 연결** · **논리 구조화**
- hexagon SVG (cx=200, cy=200, maxR=160, angles [-90,-30,30,90,150,210])
- FEEDBACK 객체에 모듈별 `radar: [v1..v6]` 사전 가중치
- Phase 3에서 LLM 의미 평가로 동적 산출 예정

### Turing Test Index (CLAUDE.md 4.4)
- 0~100 — "얼마나 인간다운가"
- Open: 자기 의심·구체화·직관 마커 + 어휘 다양성 + 문장 변동성
- MCQ/Flag: 시간/정확도 기반 약한 추정
- 5단계 정성 라벨 (매우 인간적 / 인간적 / 경계 / 기계적 경향 / 강한 기계 패턴)

### 채점 알고리즘
- **MCQ:** 가중 정답률 × 80 + 연속 정답 보너스(2/3/5연속 = 4/8/12) + 함정 정답 +5 + 어려움 정답 +3
- **Flag:** F1 score `2PR/(P+R)`
- **Open:** 길이(25) + 어휘다양성(15) + 구조마커(25) + 메타마커(20) + 문장결정성(15)
- **AA 환산:** 시그모이드 `15 + 45 / (1 + e^(-(x-50)/13))` → 모듈점수 0~100 → AA 15~60

---

## 🎨 디자인 토큰 (변경 금지)

- **색:** background `#fbf9f3` · on-surface `#1b1c19` · primary `#001cbf` · primary-fixed-dim `#bcc2ff` · error `#ba1a1a` · outline `#757689` · outline-variant `#c5c5da` · surface-container-low `#f5f4ee`
- **폰트:** Anton (display) · EB Garamond (body) · JetBrains Mono (label) · Noto Sans KR (`.kr` 클래스)
- **언어 원칙:** 본문/CTA/헤드라인 한국어, 네비/atmospheric 라벨(FILE 00, SIM // X-01, CAT 01)은 영문
- **스타일:** 라이트 + 브루탈리스트/에디토리얼. 직선·고대비·블루 포인트. 둥근 모서리 최소
- **WebGL 뇌:** 파티클 3500, pixelRatio 1.25 캡, antialias off, IntersectionObserver+visibilitychange 절전

---

## 🧠 사용자 선호 (학습된 패턴 — 매우 중요)

**1. CLAUDE.md 라인 번호 언급 시 무시할 것.** 사용자가 "293-469줄 참고" 같이 라인 번호를 댈 때가 있는데, 실제 파일은 다를 수 있음. **컨텐츠 키워드로 매핑**하고 라인 번호는 신뢰하지 말 것.

**2. 가짜 UI 절대 금지.** 동작 안 하는 필터, 의미 없는 숫자, 클릭해도 무반응 버튼은 모두 사용자가 명시적으로 지적함. **모든 표시되는 요소는 실제 동작해야 하거나 명확한 "Phase 2 예정" 라벨이 있어야 함.**

**3. 명확한 라벨 선호.** "신경 부하 52%" 같은 모호한 표현 → "체류 시간 · 이 모듈에 머문 시간" 같이 부제로 의미 명시. 직관적이지 않으면 바꾸거나 부제 추가.

**4. 정답/오답 명확히.** "정답입니다 ✓" / "틀렸습니다 ✗" 텍스트 + 색상 + 해설 3중. 색만 바뀌면 안 됨.

**5. 즉시 정답 판정 회피.** MCQ 옵션 클릭은 단순 "선택"이고 별도 "선택 확정" 버튼이 있어야 사용자가 고민할 수 있음. 클릭 즉시 정답 처리하지 말 것.

**6. 개방형 = 정답 없음.** 명세 2.2절 핵심. M-01/M-02/M-03/E-03/C-02/R-03에서 절대 "정답 풀이" 표현 쓰지 말 것. "체크포인트" "대안적 사고"가 맞는 용어.

**7. 모바일 UX 신경 쓸 것.** 모바일 simulation은 가운데(문제) 우선, HUD는 위아래 컴팩트. 단축키 hint는 데스크탑만.

**8. 작업 우선순위 묻지 말고 진행할 것.** 사용자는 "완벽하게 구현해" 같은 광범위 지시 후 능동적 진행 선호. 5건 정도는 묻지 말고 묶어서 처리. 단 정말 모호한 부분(예: 부록 A 위치)은 짧게 1회 확인 OK.

**9. 헤더 + ticker는 sticky 한 세트.** 스크롤해도 같이 따라다녀야 함. simulation.html만 ticker 제외.

**10. 한국어 우선.** 모든 본문·해설·체크포인트·대안은 한국어. 코드명·라벨만 영문.

---

## ✅ Phase 2 진입 체크리스트

**완료 (Phase 1 v0.5 final):**
- [x] 명세 v3 7개 카테고리 중 Phase 1 4개 카테고리 모두 인터랙티브 모듈 보유
- [x] 12개 모듈 (F·M·E·C·H·R) — 채점·해설·체크포인트·대안 완비
- [x] 두 갈래 채점 (명세 2.2)
- [x] AI 모델 매칭 직접 카드 (명세 2.3)
- [x] AI 풀이 시간 12 × 3 (명세 4.2)
- [x] 6축 레이더 (명세 4.3)
- [x] Turing Test Index (명세 4.4)
- [x] 로그인 placeholder 모달 (명세 1.5)
- [x] OG/Twitter 메타 + 결과 공유
- [x] 진척도 추적 + 다음 모듈 자동 추천
- [x] 키보드 단축키 (1-4/Enter/ESC/?) + 오버레이
- [x] 모바일 반응형 + 데이터 초기화
- [x] WebGL 뇌 (GPU 절전) + seamless ticker

**Phase 2 작업 (우선순위순):**
1. **모델 리더보드 외부화** — 명세 2.3 주의 사항. 현재 `LEADERBOARD = [...]` 60개 하드코딩 → JSON config 또는 API. 정기 스크래핑/수동 갱신.
2. **FastAPI 0.135+ / Python 3.12+** 백엔드 — 명세 5.2
3. **OAuth (Google · GitHub)** + Postgres 사용자/학습 이력 — 명세 1.5
4. **문제 은행 시스템** — CAT 03 부록 A-3 잔여 7문제(SQL 인젝션·has_dup·캐싱·엘리베이터·멱등성·채팅·추천) 등 모듈당 N개 풀 랜덤 출제
5. **Monaco/CodeMirror 코드 편집기** — 명세 5.1. E-01·E-02 등 코드 분석 문제용
6. **서버사이드 채점** — 명세 5.6. 현재 클라이언트 코드에 정답 노출됨 (개발자 도구로 확인 가능)
7. **AI 풀이 시간 실측 파이프라인** — 명세 C.5. 현재 mock값. 실제 API 호출 사전 측정·캐싱
8. **Tailwind CDN → PostCSS 빌드** — 명세 5.1. 첫 로드 시 JIT 200ms+ 지연

**Phase 3 (먼 미래, LLM 필요):**
- CAT 05 AI 디렉팅 모듈
- 개방형 문제 임베딩 의미 평가 (pgvector)
- 소크라테스 AI 튜터 챗봇
- 6축 레이더 동적 산출 (현재 사전 가중치)

---

## 🚀 다음 세션 시작 시 권장 첫 행동

1. **이 문서 + CLAUDE.md 읽기** (이미 함)
2. **로컬 서버로 현재 상태 확인:**
   ```bash
   cd /Users/siong/Desktop/HumanX && python3 -m http.server 8000
   # open http://localhost:8000
   ```
3. **사용자에게 다음 작업 확인:**
   - Phase 2 백엔드 진입을 시작할지 (FastAPI + OAuth + Postgres)
   - 아니면 Phase 1에 추가 작업이 있는지 (예: CAT 03 잔여 7문제 추가, 모델 리더보드 외부화 등)
4. **새 작업 받으면 TaskCreate**로 추적, 사용자 선호 #1~#10 준수

---

## 💾 메모리 시스템 (`/Users/siong/.claude/projects/-Users-siong-Desktop-HumanX/memory/`)

- `project_progress.md` — Phase 진척도 + v0.3/v0.4/v0.5 변경 누적
- `project_repo.md` — GitHub 리포 + 배포 URL
- `MEMORY.md` — 인덱스