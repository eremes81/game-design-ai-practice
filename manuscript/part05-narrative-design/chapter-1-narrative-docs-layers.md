---
title: "5.1 NarrativeDocs Layer 0~4 구조"
part: 5
chapter: 1
status: v3
version: v3
written: 2026-05-24
revised: 2026-06-06
author: 이민수
ip_check: done
---

# 5.1 NarrativeDocs Layer 0~4 구조

회의실에 들어서니 화이트보드에 캐릭터 이름 하나가 빨갛게 동그라미 쳐져 있었다. 김 모라는 NPC였다. 한 기획자의 사이드 퀘스트에서 그는 "주인공을 어릴 때 거둬 키운 양아버지"였고, 다른 기획자의 메인 퀘스트 챕터 3에서 그는 "주인공을 배신하고 떠난 옛 동료"였다. 두 문서 모두 한 달 전에 승인됐고, 둘 다 빌드에 들어가 있었다. 보이스 녹음 견적까지 받은 상태였다.

누구의 잘못도 아니었다. 두 기획자 모두 세계관 문서를 읽었고, 캐릭터 설정을 참고했다. 문제는 같은 캐릭터의 설정이 세 개의 다른 파일에 흩어져 있었고, 그중 어느 것이 "진짜"인지 아무도 단언할 수 없었다는 데 있었다. 세계관 문서는 한 덩어리짜리 70페이지 워드 파일이었고, 검색하면 김 모가 열한 군데에서 나왔다. 어떤 줄이 결정이고 어떤 줄이 메모인지 구분이 없었다.

그날 회의가 끝나고 결정한 것이 NarrativeDocs를 다섯 층으로 쪼개는 일이었다. 이 장은 그 다섯 층의 이야기다.

---

## 5.1.1 가장 추상적인 분야부터 시작하는 이유

분야별 Layer 분해를 내러티브에서 먼저 여는 데에는 이유가 있다.

내러티브는 가장 추상적이다. 세계관, 감정, 톤 같은 것들은 숫자로 떨어지지 않는다. 아트나 시스템처럼 "스프라이트 수", "데미지 계수" 같은 명확한 단위가 없다. 이렇게 추상적인 분야가 Layer로 깔끔하게 분해된다면, 더 구체적인 다른 분야들은 자연히 같은 패턴으로 풀린다. 어려운 데서 먼저 통하는지 보는 셈이다.

또 내러티브는 인터페이스가 가장 많다. 캐릭터는 아트와 닿고, 퀘스트는 콘텐츠·레벨과 닿고, 대사는 UX·현지화와 닿고, 보상은 시스템과 닿는다. 분야 사이를 가장 많이 가로지르는 자리라서, Layer 통합의 가치가 곧바로 드러난다.

마지막으로 자연어 산출물의 비중이 가장 높다. 그래서 AI 보조가 가장 크게 작동하는 분야이기도 하다. 다만 모든 게임이 내러티브 중심은 아니다. 캐주얼·아케이드 장르라면 이 장의 깊이가 과할 수 있다. 그래도 "한 덩어리 문서를 Layer로 쪼개고 인터페이스를 좁힌다"는 골격 자체는 어느 분야에든 그대로 옮겨진다.

---

## 5.1.2 다섯 칸 서랍

NarrativeDocs를 다섯 층으로 분해한 모양은 다음과 같다. 비전(L0)이 위에 있고, 빌드·QA(L4)가 아래에 있으며, 층 사이를 잇는 통로는 의도적으로 좁다.

<svg viewBox="0 0 720 520" xmlns="http://www.w3.org/2000/svg" font-family="sans-serif">
  <style>
    .layerbox { rx: 8; }
    .ltitle { font-size: 15px; font-weight: bold; fill: #1a1a2e; }
    .ldesc { font-size: 11px; fill: #444; }
    .iface { font-size: 11px; fill: #b03030; font-style: italic; }
    .owner { font-size: 10px; fill: #2a6; }
  </style>

  <!-- L0 -->
  <rect x="120" y="20" width="480" height="60" rx="8" fill="#fdeaea" stroke="#c0392b" stroke-width="2"/>
  <text x="140" y="44" class="ltitle">L0 비전 — "이 세계는 무엇인가"</text>
  <text x="140" y="64" class="ldesc">world_premise · narrative_pillar · tone_manifesto  (불변 · 약 4.5장)</text>
  <text x="560" y="44" class="owner" text-anchor="end">디렉터·리드</text>

  <!-- arrow L0->L1 -->
  <line x1="360" y1="80" x2="360" y2="108" stroke="#888" stroke-width="2"/>
  <polygon points="360,116 355,106 365,106" fill="#888"/>
  <text x="372" y="100" class="iface">pillar · tone (변경 시 L1 재검토)</text>

  <!-- L1 -->
  <rect x="120" y="116" width="480" height="60" rx="8" fill="#eef2fb" stroke="#2c5fa0" stroke-width="2"/>
  <text x="140" y="140" class="ltitle">L1 시스템 — "어떻게 작동하는가"</text>
  <text x="140" y="160" class="ldesc">faction_system · reputation_model · dialogue_branching_rule · lore_consistency_rule</text>
  <text x="560" y="140" class="owner" text-anchor="end">시니어 내러티브</text>

  <!-- arrow L1->L2 -->
  <line x1="360" y1="176" x2="360" y2="204" stroke="#888" stroke-width="2"/>
  <polygon points="360,212 355,202 365,202" fill="#888"/>
  <text x="372" y="196" class="iface">룰북·분기 정책 (영향 퀘스트 자동 목록화)</text>

  <!-- L2 -->
  <rect x="120" y="212" width="480" height="60" rx="8" fill="#eef9ee" stroke="#2e8b57" stroke-width="2"/>
  <text x="140" y="236" class="ltitle">L2 콘텐츠 — "무엇이 일어나는가"</text>
  <text x="140" y="256" class="ldesc">main_quest · side_quest · character_bible · lore_codex  (가장 두꺼운 층)</text>
  <text x="560" y="236" class="owner" text-anchor="end">기획자 다수</text>

  <!-- arrow L2->L3 (narrow!) -->
  <line x1="360" y1="272" x2="360" y2="300" stroke="#b03030" stroke-width="3"/>
  <polygon points="360,308 354,297 366,297" fill="#b03030"/>
  <text x="372" y="292" class="iface">quest_id · npc_id · dialogue_id (열 한 개)</text>

  <!-- L3 -->
  <rect x="120" y="308" width="480" height="60" rx="8" fill="#fbf5e9" stroke="#c08a2c" stroke-width="2"/>
  <text x="140" y="332" class="ltitle">L3 데이터 — "기계가 읽는 형태"</text>
  <text x="140" y="352" class="ldesc">quest_table · npc_table · dialogue_id_table · reward_table  (자연어 0줄)</text>
  <text x="560" y="332" class="owner" text-anchor="end">내러티브+데이터</text>

  <!-- arrow L3->L4 -->
  <line x1="360" y1="368" x2="360" y2="396" stroke="#888" stroke-width="2"/>
  <polygon points="360,404 355,394 365,394" fill="#888"/>
  <text x="372" y="388" class="iface">시트 변경 시 자동 lint 트리거</text>

  <!-- L4 -->
  <rect x="120" y="404" width="480" height="60" rx="8" fill="#f2eefb" stroke="#7a4fa0" stroke-width="2"/>
  <text x="140" y="428" class="ltitle">L4 빌드·QA — "출시 가능한가"</text>
  <text x="140" y="448" class="ldesc">narrative_qa_checklist · voice_review_log · localization_status</text>
  <text x="560" y="428" class="owner" text-anchor="end">내러티브+QA</text>

  <!-- side note: locked anchor -->
  <line x1="120" y1="50" x2="60" y2="50" stroke="#c0392b" stroke-width="1.5" stroke-dasharray="4 3"/>
  <line x1="60" y1="50" x2="60" y2="434" stroke="#c0392b" stroke-width="1.5" stroke-dasharray="4 3"/>
  <line x1="60" y1="434" x2="120" y2="434" stroke="#c0392b" stroke-width="1.5" stroke-dasharray="4 3"/>
  <text x="52" y="245" class="iface" text-anchor="middle" transform="rotate(-90 52 245)">L0는 매번 컨텍스트로 주입된다 (생성·검수의 앵커)</text>
</svg>

폴더로 옮기면 다음 형태다. 각 파일명은 책에서 추상화한 이름이 아니라 실제로 그 폴더에 존재하는 파일명이다.

```
NarrativeDocs/
├── Layer0_Vision/
│   ├── world_premise.md          (세계관 전제 — 불변)
│   ├── narrative_pillar.md       (감정 기둥 3개)
│   └── tone_manifesto.md         (톤·금기 어휘 목록)
├── Layer1_System/
│   ├── faction_system.md
│   ├── reputation_model.md
│   ├── dialogue_branching_rule.md
│   └── lore_consistency_rule.md
├── Layer2_Content/
│   ├── main_quest/               (챕터 단위)
│   ├── side_quest/
│   ├── character_bible/
│   └── lore_codex/
├── Layer3_Data/
│   ├── quest_table.xlsx
│   ├── npc_table.xlsx
│   ├── dialogue_id_table.xlsx
│   └── reward_table.xlsx
└── Layer4_Build_QA/
    ├── narrative_qa_checklist.md
    ├── voice_review_log.md
    └── localization_status.md
```

다섯 층을 한 사람이 책임지지 않는다는 점이 중요하다. 층마다 주 담당이 다르고, 인접한 층 사이의 통로만 표준화한다. 위 그림의 빨간 화살표가 그 통로다. 특히 L2와 L3 사이의 통로는 일부러 가장 좁게(굵은 빨간 화살표) 그려 두었는데, 그 이유는 뒤에서 본다.

서랍 비유로 보면 다섯 칸 서랍이다. 첫째 칸에는 절대 안 옮기는 세계관 한 줄, 둘째 칸에는 룰북, 셋째 칸에는 본문, 넷째 칸에는 시트, 다섯째 칸에는 검수 로그. 칸 사이 통로는 좁고, 통로 위에는 변경 알림 벨이 달려 있다.

---

## 5.1.3 L0 — 변하지 않게 만들려고 작게 쓴다

L0는 변하지 않는다. 변하면 게임의 정체성이 변하는 것이다. 그래서 분량이 작아야 한다. 작아야 안 변한다.

| 문서 | 분량 |
|---|---|
| world_premise.md | A4 1.5장 |
| narrative_pillar.md | A4 1장 (감정 3개) |
| tone_manifesto.md | A4 2장 (톤 + 금기 어휘 목록) |

합쳐 약 4.5장. 이게 L0의 무게다. 무거워지면 변경이 두려워지고, 두려워지면 다른 층이 L0를 우회하기 시작한다. 우회가 시작되면 L0는 죽은 문서가 된다.

`narrative_pillar.md`의 실제 골격은 이런 모양이다(내용은 추상화).

```markdown
---
title: 내러티브 감정 기둥
layer: L0
status: locked
last_updated: 2026-05-18
---

## 1. 잃은 것에 대한 그리움
- 플레이어가 매 챕터 끝에서 한 가지를 잃는다.
- 잃은 것은 다시 돌아오지 않는다 (회상으로만).

## 2. 의무와 자유의 갈등
- 모든 주요 NPC는 두 가지 의무를 진다.
- 플레이어의 선택은 한쪽 의무만 살릴 수 있다.

## 3. 작은 손길의 무게
- 큰 영웅적 행위보다 작은 친절이 더 큰 결과를 낳는다.
```

이 세 줄짜리 기둥이 그 아래 수백 페이지의 방향을 정한다. `status: locked`는 단순한 라벨이 아니다. L4의 자동 점검 중 하나가 이 라벨을 읽어서, locked 문서가 PR에서 수정되면 리드 내러티브의 승인 없이는 머지가 막히도록 걸어 둔다.

---

## 5.1.4 L1 — 코드와 가장 가까운 내러티브

L1은 변경 가능하지만 비용이 크다. 룰북이기 때문이다. 룰북 한 줄이 바뀌면 그 룰을 따르는 모든 콘텐츠가 영향을 받는다.

`faction_system.md`의 골격은 다음과 같다.

```markdown
---
title: 세력 시스템
layer: L1
atoms:
  - faction_relation_matrix
  - faction_membership_rule
  - faction_quest_eligibility
---

## 1. 세력 개념
N개 세력. 각 세력은 (이념, 자원, 영토)로 정의됨.

## 2. 세력 간 관계
- relation_matrix.json (-3 적대 ~ +3 동맹)
- 관계 변화 트리거: 메인 퀘스트 결정, 평판 임계

## 3. 플레이어 소속 규칙
- 동시 소속 최대 2개 (적대 관계 동시 불가)
- 탈퇴 페널티: 평판 -2, 동맹 세력 -1
```

frontmatter의 `atoms:` 목록을 눈여겨보자. 이 세 개의 atom 이름은 단순한 메모가 아니라, 7부 온톨로지와 11부 관계도가 추적하는 식별자다. 어떤 퀘스트가 `faction_quest_eligibility`를 참조하면, 이 룰이 바뀔 때 그 퀘스트가 영향 목록에 자동으로 올라온다. L1은 게임 코드와 가장 가까운 내러티브 산출물이라, 시스템 기획자와 짝지어 작업한다.

---

## 5.1.5 L2 — 가장 두꺼운 층, 본문이 사는 곳

L2는 가장 두껍다. 메인 퀘스트, 사이드 퀘스트, 캐릭터 바이블, 로어 사전이 모두 여기 산다. 앞서 회의실에서 충돌했던 "양아버지 vs 배신한 동료" 김 모의 진짜 설정도, 이제는 `character_bible/` 안의 한 파일로만 존재한다. 그 파일이 단일 진실 원천이고, 퀘스트는 거기를 참조만 한다.

메인 퀘스트 폴더는 다음 형태다.

```
main_quest/
├── chapter_01_awakening/
│   ├── 00_chapter_overview.md
│   ├── 01_quest_a_call_to_arms.md
│   ├── 02_quest_b_first_choice.md
│   └── ...
├── chapter_02_road/
│   └── ...
└── _TEMPLATES/
    └── quest_template.md
```

각 퀘스트 파일은 atom 표준 형식을 따른다.

```markdown
---
title: 무기를 들 때
layer: L2
type: main_quest
atoms:
  - quest_chapter_01_awakening_a
related:
  affects: [reputation_model, faction_relation_matrix]
  derives_from: [narrative_pillar, world_premise]
  requires: [character_kim, faction_alpha]
  part_of: chapter_01_awakening
---

## 진행 단계
1. ...

## 분기
- A안 선택 시: ...
- B안 선택 시: ...

## 보상 (L3 참조)
- reward_table.xlsx → quest_001 행
```

핵심은 `related:` 블록이다. `requires: [character_kim]`이라고 적는 순간, 이 퀘스트는 김 모의 설정을 character_bible에서 가져온다고 선언한 것이고, 더 이상 자기 파일 안에서 김 모를 새로 정의하지 않는다. 내러티브 본문은 L2에, 수치 보상은 L3 시트에 둔다. 둘이 한 파일에 있으면 시트 한 줄 고칠 때마다 본문을 건드려야 하고, 그러면 번역키가 어긋난다.

---

## 5.1.6 L3 — 자연어 한 줄도 없는 층

L3는 시트와 ID다. 자연어 문장이 한 줄도 들어가지 않는다.

```
quest_table.xlsx
| quest_id | chapter | type | unlock_level | reward_xp | reward_gold | dialogue_set_id |
|----------|---------|------|--------------|-----------|-------------|-----------------|
| q_001    | ch01    | main | 1            | 500       | 100         | ds_001          |
| q_002    | ch01    | main | 2            | 800       | 150         | ds_002          |
```

대사조차 ID로만 참조한다. 본문은 `dialogue_id_table.xlsx`에 따로 있고, 번역키와 1:1로 매핑된다. L2와 L3를 잇는 통로는 `quest_id` 단 한 열이면 충분하다. 앞 그림에서 이 통로만 굵은 빨간 화살표였던 이유가 여기 있다. 인터페이스를 한 열로 좁게 만드는 것이 Layer 분리의 핵심이다. 통로가 넓으면 양쪽이 서로를 너무 많이 알게 되고, 한쪽을 고칠 때 다른 쪽이 따라 깨진다.

---

## 5.1.7 L4 — 출하 게이트

L4는 검수와 출하다. 새 콘텐츠가 들어올 때마다 자동·수동 점검이 작동한다. 자동 점검은 스크립트로 돌린다. 아래 네 개는 실제로 CI에 걸려 있는 lint들이다.

| 검사 | 도구 |
|---|---|
| 모든 dialogue_id 매핑 존재 | `dialogue_lint.py` |
| 모든 quest_id가 chapter에 속함 | `quest_lint.py` |
| 보상 합계가 챕터별 곡선 범위 내 | `reward_curve_check.py` |
| 금기 어휘 출현 여부 | `tone_lint.py` (L0 tone_manifesto 기반) |

`tone_lint.py`가 L0의 `tone_manifesto.md`를 직접 읽는다는 점에 주목하자. 맨 위 층(불변 비전)과 맨 아래 층(출하 게이트)이 자동화로 직접 연결돼 있다. 비전에 적은 금기 어휘가 출시 직전 본문에서 검출되면 빌드가 막힌다.

자동으로 못 잡는 것은 사람이 본다.

| 검사 | 담당 |
|---|---|
| L0 감정 기둥 부합 | 리드 내러티브 |
| 캐릭터 보이스 일관성 | 캐릭터 담당 + 내러티브 |
| 현지화 가능성 | 로컬라이저 |

자동과 수동의 경계가 명확하면 검수 시간이 예측 가능해진다. "이번 챕터 검수 며칠 걸려요?"에 답할 수 있게 된다.

---

## 5.1.8 AI에게 Layer를 시켜 보다 — 워크드 트랜스크립트

여기까지가 구조다. 그런데 이 구조가 진짜로 일하는 자리는, 새 콘텐츠를 만들 때다. 이미 다섯 층이 깔린 프로젝트에서 사이드 퀘스트 한 줄짜리 아이디어를 받아 Layer로 흩뿌리는 작업을 Claude에게 시킨 실제 세션을 그대로 옮긴다. 요약하지 않고, 빗나간 부분과 거부한 부분까지 포함한다.

**보낸 프롬프트(전문):**

```
첨부한 L0/L1 컨텍스트 절대 어기지 말고 우리 Layer 구조로 분해해줘.

[narrative_pillar.md 전문 — 감정 기둥 3개]
[tone_manifesto.md 발췌 — 금기 어휘: "운명", "예언", "선택받은 자"]
[character_bible/character_kim.md 발췌 — 김: 주인공을 거둔 양아버지,
 과묵, 말끝 흐림, 감정을 직접 말 안 함]

아이디어: "김이 플레이어에게 죽은 아내의 유품을 건네는 짧은 사이드 퀘스트."

L2 퀘스트 파일(related 블록 포함, 본문 200자쯤), L3 quest_table 행이랑
dialogue_id, 그리고 tone 위반 자가 점검까지. 일단 L2만 쓰고 멈춰줘.
```

**Claude의 날것 출력(L2):**

```markdown
---
title: 빛바랜 손수건
layer: L2
type: side_quest
atoms:
  - quest_side_kim_keepsake
related:
  affects: [reputation_model]
  derives_from: [narrative_pillar]
  requires: [character_kim]
  part_of: chapter_02_road
---

## 진행 단계
1. 김이 플레이어를 조용히 부른다. 평소처럼 용건을 바로 말하지 않는다.
2. 낡은 손수건을 내민다. "이걸… 자네가 가지고 있는 게 나을 것 같아서."
3. 플레이어가 무엇이냐 물으면, 김은 대답 대신 창밖을 본다.
4. (선택) 받는다 / 사양한다.

## 분기
- 받는다: 김의 평판 +1. 이후 챕터에서 손수건 관련 회상 1회 해금.
- 사양한다: 김은 고개를 끄덕이고 손수건을 다시 넣는다. 평판 변화 없음.
  손수건은 영영 다시 등장하지 않는다.

## 보상 (L3 참조)
- reward_table.xlsx → quest_side_kim_keepsake 행
```

여기서 Claude는 멈췄고, 한 줄을 덧붙였다.

> "L0 기둥 1번(잃은 것은 다시 돌아오지 않는다)을 반영해, '사양한다'를 고르면 손수건이 영영 사라지도록 했습니다. 다만 한 가지 확인이 필요합니다. 죽은 아내 설정은 character_kim.md 발췌에 없었습니다. 제가 임의로 넣은 것이라, 캐릭터 바이블과 충돌할 수 있습니다."

**사람의 검증과 거부:**

이 출력은 톤이 정확했다. 김의 과묵함, 말끝 흐리기, 감정을 직접 말하지 않는 버릇이 살아 있었다. 금기 어휘도 없었다. 그러나 마지막 자가 점검이 정확히 진짜 문제를 짚었다. 김에게 죽은 아내가 있다는 설정은 어디에도 없었다. AI가 "유품"이라는 단어에서 자연스럽게 죽은 배우자를 추론한 것인데, 이건 바이블에 새 사실을 몰래 추가하는 일이다. 바로 이게 이 장 첫머리 회의실에서 벌어진 사고의 씨앗이다.

그래서 거부했다. 재요청을 보냈다.

**재요청:**

```
톤은 좋아. 근데 "죽은 아내"는 바이블에 없는 새 설정이라 못 써.
김 과거는 "고향 떠나며 뭘 두고 왔다"까지만 확정이야. 유품 정체를
특정하지 말고 "오래전 두고 온 것" 정도로만 흐리게 다시 써줘.
손수건도 바이블에 없으니 "천 조각" 정도로 낮추고.
```

**재요청 후 출력(발췌):**

```
2. 낡은 천 조각을 내민다. "오래전에… 두고 온 게 하나 있었네.
   이건 그 끄트머리라고만 해 두지."
3. 플레이어가 무엇이냐 물으면, 김은 대답 대신 창밖을 본다.
```

이번에는 받았다. 김의 과거를 새로 못 박지 않으면서도, 감정 기둥 1번(잃음)을 건드린다. 무엇을 잃었는지는 끝까지 흐린 채로 남는다.

이 한 세션이 보여 주는 것은 두 가지다. 첫째, Layer 컨텍스트(L0 기둥 + L1 톤 + L2 바이블)를 정확히 주입하면 AI는 톤을 놀랍도록 잘 맞춘다. 둘째, AI는 빈칸을 만나면 그럴듯하게 메운다. 그 메움이 바이블에 없는 새 사실일 때, 그걸 잡아내는 것은 여전히 사람이다. Layer 구조의 `requires: [character_kim]`이 "어디를 봐야 하는지"를 알려 줬기에, 검증자가 어느 파일과 대조할지 곧바로 알 수 있었다. 구조가 없었다면 70페이지를 다시 뒤졌을 것이다.

---

## 5.1.9 좁은 통로 위의 알림 벨

다섯 층을 나눈 진짜 이유는 인터페이스를 좁히기 위해서다. 그리고 좁은 인터페이스마다 변경 감지 자동화를 붙인다.

| 인터페이스 | 무엇이 흐르는가 |
|---|---|
| L0 → L1 | pillar, tone (변경 시 L1 룰북 재검토 트리거) |
| L1 → L2 | 룰북·분기 정책 (변경 시 영향 받는 퀘스트 자동 목록화) |
| L2 → L3 | quest_id, npc_id, dialogue_id (열 한 개) |
| L3 → L4 | 시트 변경 시 자동 lint 트리거 |

예를 들어 L1의 `faction_system.md`에서 "동시 소속 최대 2개"를 "최대 1개"로 바꾸는 PR을 올리면, 관계도가 `faction_quest_eligibility`를 참조하는 L2 퀘스트들을 훑어 영향 목록을 만들고, 그 목록이 PR 코멘트에 자동으로 첨부된다. 룰을 바꾼 사람은 "회의 두세 번 잡아서 누가 영향받는지 알아보기" 대신, 코멘트에 붙은 목록을 보고 30분 회의로 끝낸다.

핵심은 이것이다. Layer만 나누고 인터페이스가 모호하면, 칸막이만 늘어난 셈이 된다. Layer 분리 자체보다 인터페이스 자동화가 본질이다.

---

## 5.1.10 6개월 운영, 무엇이 달라졌나

다섯 층으로 옮기고 6개월을 돌린 뒤의 측정이다. 아래 수치는 저자 팀 운영 기록 기반이되 절대값은 방향·비율로만 옮긴다(저자 추정·미검증). 분리 전은 기억, 분리 후는 실측이라 같은 자료를 두 번 잰 게 아니라는 한계가 있다.

| 항목 | Layer 분리 전 | Layer 분리 후 |
|---|---|---|
| 신규 기획자 온보딩 | 3주 | 1주 |
| 룰북 변경 영향 범위 파악 | 회의 2~3번 | 자동 코멘트 + 회의 30분 |
| 새 메인 퀘스트 1챕터 제작 | 4주 | 2.5주 |
| 출시 전 1챕터 검수 | 5일 | 2일 |
| 현지화 누락 사고 | 분기당 3~5건 | 분기당 0~1건 |

가장 분명하게 줄어든 것은 현지화 누락이다. dialogue_id가 L3에서 번역키와 1:1로 묶이고 `dialogue_lint.py`가 매핑 누락을 막으면서, "번역 안 된 대사가 빌드에 들어가는" 사고가 거의 사라졌다. 온보딩이 짧아진 것도 컸다. 새 기획자에게 "70페이지 워드를 다 읽어라" 대신 "L0 4.5장만 외우고, 네 퀘스트는 L2 템플릿 채워라"라고 말할 수 있게 됐다.

한 가지 솔직하게 덧붙이면, 이 효과가 단번에 나온 건 아니다. 첫 분기에는 자동 코멘트 한 가지만 붙였고 나머지는 수작업이었다. 인터페이스 자동화는 분기마다 하나씩 늘렸다. Layer를 나누는 것보다 자동화를 붙이는 것이 더 오래 걸렸다.

---

## 5.1.11 더 깊은 이유 — 절차적 생성으로 가는 길

여기까지가 표면적 이유다. "분야 간 협업 언어를 통일한다." 그런데 더 본질적인 이유가 하나 더 있다. Layer 분해는 절차적 생성을 가능하게 만드는 전제다. 5계층 각각이 절차적 생성의 한 역할(L0 앵커 → L1 룰북 → L2 본문 → L3 수치 → L4 게이트)에 대응하고, 한 덩어리로 섞이면 생성기가 어디부터 읽고 어디에 쓸지 정하지 못해 무너진다는 일반 논제는 §6.6에서 전체로 다뤘다. 여기서는 그 전제가 내러티브 다섯 층 위에서 어떻게 실제로 작동하는지만 본다.

한 덩어리 70페이지 문서 위에서는 생성 알고리즘이 어디부터 읽고 어디에 쓸지 정할 수 없다. 내러티브 다섯 층은 그대로 생성 파이프라인의 다섯 단계가 된다 — L0 앵커, L1 입력 규칙, L2 본문이 쌓이는 자리, L3 시뮬레이션 입력, L4 검증 게이트.

앞의 워크드 트랜스크립트가 이미 이 다섯 단계의 축소판이었다. L0 기둥과 L1 톤을 컨텍스트로 주입했고(앵커), L2에 본문이 생성됐고, L3 행이 따라 나왔고, tone 위반 자가 점검이 검증 게이트 흉내를 냈다. 사람이 한 번에 한 퀘스트씩 시킨 것을, 같은 구조 위에서 generator가 사이드 퀘스트를 양산하도록 옮기면 절차적 생성이 된다.

더 멀리 가면 이렇게 흐른다 — 플레이어 행동 누적 → 월드 BT 노드 상태변화(Squad 상위) → NPC 수치변화(평판·관심사·우선순위) → NPC 태그+수치가 곧 발현 조건 → 퀘스트 클라우드에서 매칭 퀘스트 발현. 퀘스트를 미리 다 써 두는 게 아니라, 태그가 붙은 채 "공중에 떠 있는 구름"처럼 두고, 플레이어의 행동이 NPC 수치를 바꾸면 그 수치가 발현 조건과 맞는 퀘스트가 내려와 나타난다. 이 진보적 모델은 5.3에서 다시 자세히 다룬다(흐름도 포함). 여기서 강조할 점은, 이 모든 흐름이 다섯 층 분해 위에서만 작동한다는 것이다.

반대로 Layer가 섞여 있는 팀은 절차적 생성으로 가지 못한다. 시도하는 순간 일관성 사고로 무너진다. 김 모가 양아버지이자 배신자가 되는 그 사고가, 생성기를 통해 자동으로 양산된다고 상상해 보면 된다.

다만 처음부터 다섯 칸 서랍을 완벽히 갖춰야 한다는 뜻은 아니다. 첫 분기에는 L0 한 줄과 L1 룰북 한 권만 분리해도 충분하다. 분리는 점진적으로, 인터페이스는 좁게다.

마지막으로 시점에 관한 한 가지. Layer 분해 자체는 결정론적 PCG(Procedural Content Generation, 절차적 콘텐츠 생성) 시절부터 있던 분리다. 새로운 것은 LLM이 그 분리 위에서 자연어 본문·페르소나·서사 분기까지 처리하게 됐다는 점이다 — 위 트랜스크립트에서 AI가 김의 톤을 맞춰 대사를 쓴 일은 5년 전 룰 테이블로는 불가능했다. 이 시점론은 5.3에서 더 다룬다.

다음 장(5.2)에서는 이 다섯 층 위에서 `lore_consistency_rule`이 어떻게 세계관→캐릭터→퀘스트 일관성을 자동으로 검증하는지, 즉 김 모 사고를 구조적으로 막는 검사기를 본다.

---

## 따라하기 — 첫 Layer 분해

이미 한 덩어리 세계관 문서가 있는 상태에서 시작한다고 가정합니다.

**setup.** NarrativeDocs 폴더 아래 빈 다섯 폴더를 만드세요. `Layer0_Vision`부터 `Layer4_Build_QA`까지입니다. 기존 한 덩어리 문서는 그대로 두고, 여기서 "절대 안 변하는 한 줄"만 골라 `Layer0_Vision/narrative_pillar.md`에 옮깁니다. frontmatter에 `status: locked`을 입력합니다. 이 한 파일이 4.5장을 넘지 않게 합니다.

**prompt.** 새 콘텐츠를 만들 때 AI에게 이 순서로 컨텍스트를 줍니다.

```
[narrative_pillar.md 전문]
[tone_manifesto.md 금기 어휘]
[관련 character_bible 파일 발췌]

아이디어: "<한 줄 아이디어>"

이 컨텍스트 어기지 말고 L2 퀘스트 파일부터 써줘. related 블록
(requires/derives_from/affects) 채우고, 바이블에 없는 새 설정은
넣지 말고 필요하면 멈춰서 물어봐.
```

**verify.** 출력에서 두 가지를 보세요. (1) `requires:`에 적힌 파일을 실제로 열어, AI가 거기 없는 사실을 새로 만들지 않았는지 대조합니다. (2) 금기 어휘를 본문에서 검색합니다(`tone_lint.py`가 있으면 자동, 없으면 눈으로). 둘 중 하나라도 걸리면 거부하고, 무엇이 틀렸는지 명시해 재요청하세요. 위 트랜스크립트에서 "죽은 아내"를 거부한 것이 바로 (1)입니다.

---

## 5.1.12 1인 축소판

팀 없이 혼자 만드는 인디 개발자라면 다섯 층이 과해 보일 수 있습니다. 두 칸이면 됩니다.

`vision.md` 한 장(L0+L1 합침)과 `content/` 폴더 하나(L2), 그리고 스프레드시트 한 장(L3)을 둡니다. QA는 별도 층 대신, content 파일 frontmatter에 `requires:` 한 줄만 적는 습관으로 대신하세요. 새 퀘스트를 쓸 때마다 `requires`에 적은 파일만 다시 펼쳐 대조하면, 70페이지를 다 뒤지지 않고도 김 모 사고를 막을 수 있습니다. 핵심은 층의 개수가 아니라, "절대 안 변하는 한 줄을 따로 떼어 매번 AI에게 먼저 보여 주는" 습관입니다. 그 한 줄이 컨텍스트 앵커이고, 1인이든 중규모 팀이든 거기서부터 시작합니다.

---

### 이 챕터의 핵심 메시지

- 가장 추상적인 내러티브가 Layer로 풀리면 다른 분야는 같은 패턴으로 따라온다.
- L0는 작아야 안 변하고, 안 변해야 생성·검수의 컨텍스트 앵커가 된다.
- Layer를 나누는 것보다 좁은 인터페이스에 자동화를 붙이는 것이 본질이다.
