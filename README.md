# HUMAN/X

> Training humanity in the AI era.

AI가 아직 닿지 못한 **맥락 이해**와 **비선형적 사고**를 훈련하는 MVP 인터페이스입니다.
지식이 아니라 판단을, 정답이 아니라 구조를 학습합니다.

**Live demo:** https://timidlione.github.io/humanx/

## Pages

| File | Role |
| --- | --- |
| `index.html` | Landing — 3대 사고 축(α/β/γ) · 시뮬레이션 · 벤치마크 소개 |
| `modules.html` | 6개 훈련 모듈 카탈로그 (Cognition × 3, Simulation × 3) |
| `simulation.html` | HUD-스타일 인터랙티브 시뮬: AI 환각 감별 인터뷰 (Mock 시나리오) |
| `benchmark.html` | Turing Test Index · 인간-AI 역량 레이더 · 모델별 비교 |
| `2.html` | 초기 디자인 레퍼런스 (HUD 프로토타입) |

## Stack

- 정적 HTML + Tailwind CDN
- 폰트: Anton (display) · EB Garamond (body) · JetBrains Mono (label) · Noto Sans KR
- 외부 빌드 도구 없음 — 브라우저에서 바로 열림

## Phase

**Phase 1 — MVP (현재):** 프론트엔드 + Mock 데이터로 UX 흐름 검증
**Phase 2:** 백엔드(FastAPI) · OAuth · 문제 은행
**Phase 3:** LLM 실시간 채점 · 소크라테스식 AI 튜터 챗봇

## Local Preview

```bash
python3 -m http.server 8000
# open http://localhost:8000
```
