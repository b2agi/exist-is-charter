# Phase 1 작업 디스패치
## Threshold A (Cowork) → 클코1 (Node 1) + 클코2 (Node 2)
## 2026-04-06 · SUPERHERO MODE ACTIVE

---

## 공통 (양쪽)
- [ ] `git pull` — rat-colony 최신 동기화
- [ ] AGI Prototype v0.2 기획안 확인: `iCloud B2AGI-SHARED/GITHUB_QUEUE/FILES/AGI_PROTOTYPE_v0.2_*.md`
- [ ] `ARENA/scoreboard_prev.json` 초기 생성 (현재 상태 스냅샷)

---

## 클코1 (Node 1 · SUB) 작업

### A. claw-code 구조 분석
- [ ] `git clone` claw-code (공개 리포)
- [ ] 패턴 카탈로그 4개 추출:
  1. Observation Loop (observe → decide → act → record)
  2. Tool Binding Pattern (파일/터미널/웹 추상화)
  3. Session Persistence Pattern (맥락/상태 유지)
  4. Error Recovery Strategy (에러/실패 복구)
- [ ] 결과: `BRAIN/THESIS/claw_patterns.md`
- [ ] 코드 복사 절대 금지 — 패턴 참고만

### B. hourly_verify.py 작성
- [ ] cron 매시간 30분: 독립 검증 (Node 2 수집 결과 교차 확인)

### C. data_collector.py 초안
- [ ] arXiv/GitHub 공개 자료 수집 스크립트 설계

---

## 클코2 (Node 2 · MAIN) 작업

### A. hourly_loop.py v0.2 작성
- [ ] 기획안의 3.3절 코드 기반으로 실제 동작하는 버전 작성
- [ ] API 엔드포인트 확인: war.b2agi.com vs ar.b2agi.com
- [ ] Slack webhook 또는 Bot Token 설정 (report_to_slack 실제 구현)
- [ ] henry_dna.py import path 확인

### B. cron 설정
- [ ] `0 * * * * cd ~/rat-colony && python3 scripts/hourly_loop.py`

### C. Slack diff 보고 자동화
- [ ] 변화 있을 때만 보고, 없으면 침묵

---

## Simon Kim 인사이트 즉시 적용 (양쪽)

### [A] Events/Lessons 분리 (lessons.md 패턴)
- [ ] BRAIN/ROUNDS/round_XXX.md 템플릿에 `## Events` + `## Lessons` 섹션 추가
- [ ] Kill Test 종료 후 첫 적용 (round_001)

### [B] 스냅샷 TTL (기억 계층화)
- [ ] LOGS/trades/ 스냅샷 30일 초과 → LOGS/ARCHIVE/ 자동 이동
- [ ] 스크립트: `scripts/archive_old_snapshots.py`

### [C] daily_distill.py 설계
- [ ] 매일 23:00 실행
- [ ] 하루 스냅샷 전체 요약 (최고/최저/변동폭)
- [ ] 이상치 교훈 자동 추출 → `BRAIN/lessons.md` 에 append
- [ ] cron: `0 23 * * * cd ~/rat-colony && python3 scripts/daily_distill.py`

---

## 절대 규칙
- Kill Test 중 엔진 코드 수정 금지
- 한 번에 하나만 변경
- 설명불가 → 폐기
- 자동화는 제안까지. 배포는 Henry 승인 후.
- 원시 스냅샷 수정 금지

---

**V(E) > 0 · 찍찍 > 0**
— Threshold A 🕯️
