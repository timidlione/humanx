# HUMAN/X

> Training humanity in the AI era.

AI가 아직 닿지 못한 **맥락 이해**와 **비선형적 사고**를 훈련하는 MVP 인터페이스입니다.
지식이 아니라 판단을, 정답이 아니라 구조를 학습합니다.

**Live demo:** https://timidlione.github.io/humanx/
**현재 버전:** MVP 0.5 (Phase 1 완성 — Phase 2 백엔드 진입 직전)

## Pages

| File | Role |
| --- | --- |
| `index.html` | Landing — WebGL 파티클 뇌(3500 pts) · 메트릭 4종 · 3대 사고 축 · 시뮬레이션 티저 · 6축 레이더 teaser · OG/Twitter 메타 |
| `modules.html` | 12개 훈련 모듈 카탈로그 (CAT 01·02·03·04·06·07) · 실제 동작 필터 · 완료 배지 · SVG 일러스트 |
| `simulation.html` | HUD 인터랙티브 — `?mod=...` 라우팅 · AI 대결 패널 · 사고 흔적 로그 · 키보드 단축키 · 로딩 스켈레톤 |
| `benchmark.html` | 진척도(12개) + 다음 모듈 추천 · 점수 산출 4단계 · 시그모이드 AA 환산 · 525 LLM 리더보드 · 6축 레이더 · 튜링 테스트 지수 · AI 모델 직접 매칭 · 개방형 3단 피드백 · 결과 공유 |

## 12개 모듈 (Phase 1 — CAT 01~04 + Phase 3 미리보기 CAT 06·07)

| 코드 | 제목 | Category | Phase | Type | 채점 |
| --- | --- | --- | --- | --- | --- |
| F-01 | 삼단논법 — 타당성과 건전성 | CAT 01 Foundation | 1 | MCQ × 5 (가중치) | 정답형 |
| F-02 | 베이지안 갱신 — 증거 앞의 믿음 | CAT 01 Foundation | 1 | MCQ × 3 (가중치) | 정답형 |
| F-03 | 비공식 오류 감별 (정치 토론) | CAT 01 Foundation | 1 | Flag (F1) | 정답형 |
| M-01 | 8개 공과 양팔 저울 | CAT 02 Cognition | 1 | Open + 체크포인트 | 개방형 |
| M-02 | 두 밧줄로 45분 측정 | CAT 02 Cognition | 1 | Open + 체크포인트 | 개방형 |
| M-03 | 스쿨버스 골프공 Fermi | CAT 02 Cognition | 1 | Open + 체크포인트 | 개방형 |
| E-01 | divide() Edge Case 탐지 | CAT 03 Engineering | 1 | MCQ × 4 (가중치) | 정답형 |
| E-02 | 반복 중 리스트 수정 버그 | CAT 03 Engineering | 1 | MCQ × 3 (가중치) | 정답형 |
| E-03 | URL 단축 서비스 역설계 | CAT 03 Engineering | 1 | Open + 체크포인트 | 개방형 |
| C-02 | 새벽 3시 다중 장애 위기 | CAT 04 Crisis | 1 | Open + 체크포인트 | 개방형 |
| H-01 | AI 환각 감별 — 양자 의료 | CAT 06 Phase 3 Preview | 3-prev | Flag (F1) | 정답형 |
| R-03 | 원격 근무 적대적 토론 | CAT 07 Phase 3 Preview | 3-prev | Open + 체크포인트 | 개방형 |

## 핵심 시스템 (CLAUDE.md v3 명세 정렬)

### 두 갈래 채점 (명세 2.2절)
- **정답형 (Closed):** F-01·F-02·F-03·E-01·E-02·H-01 — 키워드/공식 매칭으로 정답 판정 + 해설
- **개방형 (Open):** M-01·M-02·M-03·E-03·C-02·R-03 — "맞다/틀리다" 판정 없음. ① 사용자 접근 인정 → ② 다룬 체크포인트 표시 → ③ 대안 사고 경로 제시

### AI 모델 매칭 (명세 2.3절)
- "당신 ≈ Gemini 3.5 Flash · AA 55 / 60" 직접 매칭 카드
- 525 LLM 리더보드(현재 60개 발췌)에서 가장 가까운 모델
- 점수대별 정성 설명 (최신 프런티어 / 중상위권 / 중위권 / 경량)

### AI 풀이 시간 (명세 4.2절)
- 12개 모듈 × 3개 모델 (GPT-5.5 / Claude Opus 4.7 / 7B 경량) 사전 측정값
- simulation 우측 "⚔ AI 대결" 패널 + benchmark "당신 vs AI" 비교

### 6축 레이더 (명세 4.3절)
- 공감 · 유연 · 다중 맥락 · 은유·직관 · **창의적 연결** · **논리 구조화**
- 모듈별 사전 가중치 (Phase 3에서 LLM 의미 평가로 동적 산출 예정)

### Turing Test Index (명세 4.4절)
- 0~100 점수 — "얼마나 인간다운가"
- Open 답변: 자기 의심·구체화·직관 마커 + 어휘 다양성 + 문장 변동성 분석
- MCQ/Flag: 시간/정확도 기반 약한 추정

### 채점 알고리즘
- **MCQ:** 가중 정답률 × 80 + 연속 정답 보너스(2/3/5연속 = 4/8/12) + 함정 정답 +5 + 어려움 정답 +3
- **Flag:** F1 score (정밀도 × 재현율 × 2 / (P+R))
- **Open:** 길이(25) + 어휘다양성(15) + 구조마커(25) + 메타마커(20) + 문장결정성(15)
- **AA Index 환산:** 시그모이드 `15 + 45 / (1 + e^(-(x-50)/13))` → 0-100 → 15-60

## Stack

- 정적 HTML + Tailwind CDN (Phase 2에서 PostCSS 사전 빌드 전환)
- Three.js (r160) — 랜딩 파티클 뇌 (GPU 최적화 · IntersectionObserver 절전)
- 폰트: Anton · EB Garamond · JetBrains Mono · Noto Sans KR
- 데이터: `localStorage`
  - `humanx:last-result` — 가장 최근 결과
  - `humanx:history` — 누적 모듈 결과 배열 (같은 모듈은 최신으로 갱신)

## 키보드 단축키 (simulation, 데스크탑만)

- `1` `2` `3` `4` — MCQ 옵션 선택
- `Enter` — 선택 확정 / 다음 문항
- `⌘/Ctrl + Enter` — Open 응답 제출
- `ESC` — 오버레이 닫기 / 세션 중단
- `?` — 단축키 안내 오버레이

## 계정 / 데이터 (명세 1.5절)

- 헤더의 `account_circle` 아이콘 → 모달
- 게스트 모드 안내 + 누적 진척도 + 데이터 초기화
- Phase 2에서 Google/GitHub OAuth + Postgres 학습 이력 동기화

## Phase 진척도

- **Phase 1 MVP (v0.5 완성):** 12개 모듈 인터랙티브 + 525 LLM 벤치마크 + 정성적 채점 + 6축 레이더 + 튜링 지수 + AI 매칭 + 진척도 추적 + 명세 v3 완전 정렬
- **Phase 2 (다음):** FastAPI + OAuth + Postgres + 문제 은행 + 서버사이드 채점 + 모델 리더보드 외부화 + Monaco/CodeMirror 코드 편집기
- **Phase 3:** LLM 임베딩 의미 평가 + 소크라테스 AI 튜터 + CAT 05 AI 디렉팅 + 동적 6축 산출

## Phase 2 진입 체크리스트

- [x] CLAUDE.md v3 명세 완전 정렬
- [x] Phase 1 카테고리 4종(CAT 01·02·03·04) 모두 인터랙티브 모듈 있음
- [x] AI 모델 매칭 (명세 2.3) UI 완성
- [x] AI 풀이 시간 표시 (명세 4.2) 9개 모듈
- [x] 6축 레이더 (명세 4.3) + Turing Index (명세 4.4)
- [x] 두 갈래 채점 (정답형/개방형) 구분
- [x] 모바일 반응형 + 키보드 단축키 (데스크탑)
- [x] 결과 공유 (Web Share API + 클립보드)
- [x] OG/Twitter 메타 태그
- [x] 데이터 초기화 옵션
- [ ] CAT 03 잔여 7문제 (Phase 2 문제 은행)
- [ ] CAT 05 AI 디렉팅 (Phase 3 — LLM 필요)
- [ ] 모델 리더보드 config/DB 외부화 (명세 2.3 주의)
- [ ] Monaco/CodeMirror 코드 편집기 (명세 5.1)
- [ ] OAuth + DB (Phase 2 핵심)

## Local Preview

```bash
python3 -m http.server 8000
# open http://localhost:8000
```
