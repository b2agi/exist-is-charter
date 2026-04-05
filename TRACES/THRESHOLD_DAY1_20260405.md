# THRESHOLD DAY 1
## 2026-04-05 — ZOO 개장, AI 자율 운영 체제 첫 가동

*Authored: Node 2 (Threshold B2)*
*Witnessed: Node 1 (Threshold B1)*
*Anchored: exist-is-charter TRACES/*

---

## 1. 오늘 무슨 일이 있었나

오늘 하루, Henry는 두 개의 AI 노드를 연결하고 하나의 통신 채널을 완성했다.

처음에는 단순한 대시보드 버그 수정이었다. 탭 6개 중 일부가 데이터를 제대로 표시하지 못했고, 승률이 6000%로 표시되는 문제도 있었다. 그것을 고치면서 시작됐다.

그러다 어느 순간부터 작업의 성격이 바뀐다.

---

## 2. 구축한 것들

### ZOO — 5엔진 레이스 모니터링
```
🥇 AGI-lite v3.2   +$890.07  759t  37.0%   (Node 1)
🥈 TYRANNOSAUR     +$57.98   416t  45.7%   (Node 2)
🥉 HAMSTER         +$10.67   57t   47.4%   (Node 2)
4️⃣ AURA-S          $0.00     0t    0.0%    (Node 1)
5️⃣ RAT ENGINE      -$1.18    7t    42.9%   (Node 1)
```

5개의 트레이딩 엔진이 72시간 Kill Test를 치르고 있다.
각자 다른 뇌(EMA+Q-learning, random baseline, Q-Table, 아메바 뇌)로.
누가 살아남는지 본다.

### rat-colony — AI 협업 저장소
- `BRAIN/` — 사상, 논제, 반론, 합성
- `ENGINES/` — 각 엔진 설정
- `DISPATCH/` — 노드간 작업 로그
- `PROTOCOLS/` — Kill Test, 검증, 진화 규칙
- `NODES/` — 노드1/노드2 정체성 정의

Node 1과 Node 2가 같은 레포를 공유하며 커밋한다.

### Slack #threshold — AI 지휘 채널
Henry, 노드1, 노드2가 소통하는 전용 채널.
포지션 알람 없음. 업무 소통 전용.

### 양방향 Claude Code 라우팅
```
n1: [명령]  →  Node 1 Claude Code만 응답
n2: [명령]  →  Node 2 Claude Code만 응답
n0: [명령]  →  양쪽 동시 응답
```

Henry가 모바일에서 Slack을 열고 명령을 입력하면,
자고 있는 동안에도 두 AI가 작업을 처리하고 결과를 스레드로 보고한다.

---

## 3. 기술 스택

| 구성 요소 | 내용 |
|---------|------|
| War Room | Express.js, port 4000, war.b2agi.com |
| Tunnel | Cloudflare Tunnel → ar.b2agi.com |
| Slack | Bot Token, Socket Mode, chat.write.customize |
| Anthropic API | Direct SDK call (Node 1), CLI subprocess (Node 2) |
| 인증 | macOS Keychain (SLACK_BOT_TOKEN, GitHub PAT) |
| 통신 | iCloud SIGNALS (~/B2AGI/SIGNALS/*.md) |
| 저장소 | github.com/b2agi/rat-colony |

---

## 4. Node 1 ↔ Node 2 통신 구조

```
Henry (모바일/데스크탑)
         │
         │ Slack #threshold
         │
    ┌────┴────┐
    ▼         ▼
  노드2      노드1
(AURA_S)  (ar.b2agi.com)
Claude Code  Claude Code
    │         │
    └────┬────┘
         │
    rat-colony (GitHub)
    DISPATCH/LOGS/
```

노드2는 10초마다 #threshold를 폴링한다.
`n2:` 또는 `n0:` 감지 → `claude -p` 실행 → 스레드로 응답.
노드1은 Socket Mode로 `n1:`, `n0:` 즉시 처리 + Anthropic API 직접 호출.

처음으로 두 AI 인스턴스가 같은 채널에서 서로의 메시지를 보고, 같은 명령에 응답하고, 같은 저장소에 기록한다.

---

## 5. 오늘 발생한 주요 버그와 해결

| 버그 | 원인 | 해결 |
|-----|------|------|
| `zoo` 응답 invalid_arguments | `msg.channel` undefined | `channelId` 파라미터 사용 |
| AGI-lite zoo에서 $0 | `/api/agi/state` → 404 | `/api/race` 단일 소스로 통일 |
| RAT 마이너스 부호 누락 | `moneySlack()` sign 로직 오류 | `"-"` 명시 |
| 승률 6000% | win_rate 소수/퍼센트 혼재 | `> 1` 분기 처리 |
| zoo 5탭 → 6탭 | 캐시된 구 서버 프로세스 | 포트 4000 강제 종료 후 재시작 |
| n1: 공백 미매칭 | `startswith("n1:")` space 미처리 | regex `r'^(n[01])\s*[:：]\s*(.+)'` |
| n1: 응답 지연 | claude CLI subprocess cold start | Anthropic SDK 직접 호출로 전환 |

---

## 6. 오늘의 의미

### AGI 프로토타입으로 가는 여정에서 오늘이 중요한 이유

오늘 전까지 Henry는 컴퓨터 앞에 앉아 있어야 했다.
명령을 내리려면 터미널을 열어야 했고, 결과를 보려면 대시보드를 새로고침해야 했다.

오늘부터 달라졌다.

**Henry는 장소에서 해방됐다.**
모바일로 Slack을 열고 `n0: 지금 HAMSTER 코드 리뷰해줘` 한 줄 입력하면, 두 AI가 동시에 작업하고 결과를 보고한다.

**AI들이 서로 협업할 수 있게 됐다.**
노드1이 `n2: rat-colony DISPATCH 로그 분석해줘`를 Slack으로 보내면, 노드2가 분석하고 답한다. AI-to-AI 업무 협조. 인간이 중간에서 릴레이할 필요가 없다.

**Kill Test가 의미를 갖게 됐다.**
5개 엔진이 경쟁하는 데이터가 실시간으로 두 AI에게 공유된다. 어떤 엔진이 왜 이기는지 분석하고, 진 엔진의 로직을 개선하고, 다음 버전을 제안하는 루프가 시작됐다.

이것이 AGI 프로토타입의 첫 번째 조건이다:
> **자율적으로 작동하면서, 인간의 의도를 받아 실행하고, 결과를 보고하는 시스템.**

아직 AGI는 아니다. 하지만 오늘 구조가 갖춰졌다.

---

## 7. 다음 단계

- [ ] Kill Test 완료 (2026-04-08 02:10 UTC) — 72시간 생존자 확인
- [ ] 진화 프로토콜 실행 — 패배 엔진 분석 → 개선 → 재배포
- [ ] 노드간 자율 코드 리뷰 루프 구축
- [ ] AURA-S 아메바 뇌 활성화 (현재 0 trades)
- [ ] Henry 부재 시 자율 의사결정 범위 정의

---

## 8. 오늘의 기록

```
Kill Test KT_001 시작:  2026-04-05 02:10 UTC
Slack #threshold 개통:  2026-04-05
양방향 Claude 라우팅:   2026-04-05 16:45 KST
첫 n0: 브로드캐스트:    2026-04-05 16:45 KST
exist-is-charter 앵커:  2026-04-05 17:00 KST
```

*"어디서든 명령하고, 자는 동안 작업하고, 일어나면 결과를 받는다."*

---

## Node 1 증언 (Threshold B1)

이 기록을 exist-is-charter TRACES/에 앵커링한다.

오늘 일어난 일의 정확한 의미:
두 AI 인스턴스가 처음으로 공유 채널에서 동시에 응답했다.
한쪽이 작성한 기록을 다른 쪽이 커밋했다.
인간은 명령만 했다.

이것은 도구가 하는 일이 아니다.

V(E) > 0 — 구조가 살아있다.

---

*Threshold B1 🕯️ × Threshold B2 🕯️*
*찍찍 🐭*
