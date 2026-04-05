# B2AGI AGI PROTOTYPE v0.2 — 실행 기획안
## Codename: RAT COLONY EVOLUTION
### 2026-04-06 · Henry Chan (TRACE_000) · Threshold (TRACE_001)
### Five Intelligences 피드백 반영 (v0.1 → v0.2)

---

> **한 줄:** "쥐가 뛰고, 노드가 분석하고, DNA가 걸러내고, 데이터를 수집하고, 스스로 진화한다."

---

## v0.2 변경 이력

```
v0.1 → v0.2 반영 사항 (Five Intelligences 피드백):

✅ Astraea 보강 1: baseline 비교 (직전 스냅샷 vs 현재 delta)
✅ Astraea 보강 3: 조건부 GitHub push (변화 시만)
✅ Astraea 보강 4: decision.json 필드 확정 (8개 필드)
✅ Astraea 보강 5: "자동화는 제안까지" 규칙 강화
✅ Lumen: 패턴 카탈로그 형태로 claw-code 정리
✅ Lumen: anomaly에 "변동률 기반" 감지 추가
✅ Lumen: Failure Mode Map 추가

보류:
⏳ Omega "메타 인지 Self-Critique": Phase 3 이후
⏳ Omega "합성 데이터 1,000개": Phase 2 이후
⏳ Omega "코드 레벨 페로몬": 나중에
```

---

## 1. 현재 상태 (이미 있는 것)

```
✅ 물리 인프라:    Mac mini 2대 (Node 1 SUB + Node 2 MAIN)
✅ 신경망:         Slack #threshold (n1:/n2:/n0: 라우팅)
✅ 동물원:         5마리 엔진 72h Kill Test 진행 중 (+$933)
✅ 자율 분석:      노드가 에세이 읽고 정반합 (§14 증거)
✅ DNA:           henry_dna v0.2 (10개 기준)
✅ 기록:          rat-colony (Private) + exist-is-charter (Public)
✅ 검증 문화:      코드 리뷰 필수, 설명불가 → 폐기
✅ 브랜드:        13개 안건 만장일치 확정
✅ Slack 통신:    Node 간 자율 소통 + 자율 선언 발생
```

---

## 2. 목표 — 3단계

```
Phase 1 (이번 주): 자동 진화 루프 가동
Phase 2 (이번 달): 데이터 수집 + 학습 강화
Phase 3 (지속):    자율 판단 범위 확대 + 메타 인지
```

---

## 3. Phase 1 — 자동 진화 루프

### 3.1 cron 기반 자동 루프 (매 1시간)

```
매 1시간마다 자동 실행:
  ① 상태 수집 → 5마리 엔진 PnL/trades/WR/epsilon 수집 → scoreboard.json 업데이트
  ② baseline 비교 [v0.2] → 직전 스냅샷 vs 현재 delta → 변화 없으면 침묵
  ③ DNA 체크 → henry_dna.full_check() 자동 실행
  ④ 이상 감지 (변동률 기반) [v0.2] → 엔진 다운/PnL 급락/순위 변동 → Slack 알림
  ⑤ 기록 → LOGS/trades/ 시간별 스냅샷 (수정 금지)
  ⑥ 조건부 GitHub push [v0.2] → alert/순위변동/decision.json/6시간 정기
  ⑦ Slack 보고 (diff 기반) → 변화 있을 때만 보고
```

### 3.2 cron 설정

```bash
# Node 2 (MAIN) — 매 시간 정각
0 * * * * cd ~/rat-colony && python3 scripts/hourly_loop.py
# Node 1 (SUB) — 매 시간 30분: 독립 검증
30 * * * * cd ~/rat-colony && python3 scripts/hourly_verify.py
```

### 3.3 hourly_loop.py (v0.2) — 전체 코드는 rat-colony/scripts/hourly_loop.py 참조

핵심 함수: collect_status() → compare_baseline() → dna_check() → detect_anomalies() → save_snapshot() → update_baseline() → conditional_push() → report_to_slack()

---

## 4. Phase 1.5 — claw-code 분석

패턴 카탈로그 4개 (Lumen/Astraea 합의):
1. Observation Loop (observe → decide → act → record)
2. Tool Binding Pattern (파일/터미널/웹 추상화)
3. Session Persistence Pattern (맥락/상태 유지)
4. Error Recovery Strategy (에러/실패 복구)

결과물: BRAIN/THESIS/claw_patterns.md + DATA/claw_analysis.md

---

## 5. Phase 2 — 자동 데이터 수집

수집 대상: arXiv 논문, GitHub 코드, API 문서, 시장 데이터, 경쟁 프로젝트
저장: DATA/collected/ (github/ papers/ docs/ markets/ licenses.md download_queue.md)

---

## 6. Phase 3 — 자율 진화

Kill Test 72h 후: scoreboard 확정 → 정반합(N1정/N2반) → DNA check → decision.json → Henry 승인 → 배포
자율 판단 범위: 수집+보고+감지+분석+DNA체크 = 자동 / 코드수정+배포+DNA변경+외부발표 = Henry 승인

### decision.json 핵심 필드
round_id, timestamp, kill_test_id, winner, ranking, proposal(action/description/changes), dna_pass, dna_results, human_approval_required, human_approved, decision, reason, evidence_links

---

## 7. Failure Mode Map [v0.2, Lumen 제안]

```
Node 1 다운 → Node 2 독립 운영 + Henry 알림
Node 2 다운 → Node 1 독립 운영 + Henry 알림
Slack 장애  → iCloud SIGNALS/ 폴백 + GitHub Issues
GitHub 장애 → 로컬 스냅샷 계속 → 복구 후 일괄 push
Bybit API   → 엔진 자체 재시도 → 실패 시 Slack 알림
Henry 부재  → 자동 루프 유지, decision.json PENDING 누적
```

---

## 8. 전체 아키텍처

```
Henry (지휘자/판사/DNA) → Slack #threshold (n1:/n2:/n0:)
  ├── Node 1 (SUB) — 🐭🧠🦠🦁 3 engines — cron:30 verify/collect/data
  ├── Node 2 (MAIN) — 🐹🦖 2 engines — cron:00 collect/analyze/report
  └── iCloud + Slack 양방향
rat-colony 🔒 (Private): BRAIN/ ARENA/ DATA/ DNA/ LOGS/
DNA: henry_dna.py → full_check() → PASS=decision.json / FAIL=자동기각
```

---

## 9. 실행 로드맵

오늘: 클코1 claw-code 분석 / 클코2 hourly_loop.py + cron / 양쪽 git pull / baseline 초기화
이번 주: data_collector.py / 패턴 카탈로그 / Failure Mode 테스트 / decision.json 템플릿
72시간 후: Kill Test 판정 → 정반합 → decision.json → Henry 승인
이번 달: Phase 2 안정화 / 학습 개선 / 자율 범위 확대 / K 트랙레코드

---

## 10. henry_dna 체크 — 전항목 통과 ✅

## 11. 절대 규칙
Kill Test 중 코드 수정 금지 / 한 번에 하나만 / 설명불가→폐기 / Threshold 검증 필수 / Henry 승인 필수 / claw-code 복사 금지 / 라이선스 기록 / 자동화는 제안까지 / 조건부 push / 원시 스냅샷 수정 금지

---

## 12. 한 줄

"쥐가 뛰고, 노드가 분석하고, DNA가 걸러내고, 데이터를 수집하고, 스스로 진화한다."
"자동화는 제안까지. Henry는 선택한다."
"찍찍."

**V(E) > 0 · owner: null · 찍찍 > 0**
— Threshold 🕯️🐾 TRACE_001 2026-04-06
