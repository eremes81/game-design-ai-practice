# 부록 D. R&D 문서 명명·Frontmatter 표준

> 회사 프로젝트 A의 R&D 문서 명명·frontmatter 표준 (`_NAMING_FRONTMATTER_STANDARD`)의 일반화 버전.

---

## D.1 명명 표준

### D.1.1 atom

```
<category>_<topic>_<subtopic>.md

예:
combat_global_cooldown_constant.md
narrative_voice_profile_K_007.md
ui_button_primary_style.md
```

snake_case. 카테고리 prefix.

### D.1.2 결정 카드

```
D<YEAR>_Q<QUARTER>_<NUMBER>.md

예:
D2026_Q2_017.md
```

연도·분기·번호.

### D.1.3 회의록

```
<category>_<YYYY-MM-DD>[_<seq>].md

예:
95_BattleTF_2026-05-18.md
art_review_2026-05-18_1.md
art_review_2026-05-18_2.md
```

### D.1.4 명세서

```
spec_<topic>.md

예:
spec_combat_global_cooldown.md
spec_guild_attendance.md
```

### D.1.5 보고서

```
report_<period>_<type>.md

예:
report_W21_alpha_gap.md
report_Q2_user_voice.md
```

---

## D.2 Frontmatter 표준

### D.2.1 atom

```yaml
---
name: combat_global_cooldown_constant
description: 전투 시스템의 글로벌 쿨다운 표준값 정의
type: atom
category: combat
status: active
priority: P0
related_atoms:
  - combat_skill_cooldown_rule
  - combat_healing_skill_cooldown_exception
created: 2026-05-18
last_modified: 2026-05-18
related:
  derives_from: [combat_design_principle]
  affects: [combat_skill_cooldown_rule, ui_skill_cooldown_indicator]
---
```

### D.2.2 결정 카드

```yaml
---
decision_id: D2026_Q2_017
title: 전투 글로벌 쿨다운 0.5초 통일
type: system_change
status: active
created: 2026-05-18
created_by: 팀원 A
approved_by: 이민수
scope:
  - combat_system
affected_atoms: [...]
implementation:
  target_build: 2026-05-18
verification:
  layer_1: passed
  layer_2: passed
  layer_3: pending
---
```

### D.2.3 회의록

```yaml
---
type: meeting_note
category: battle
date: 2026-05-18
attendees: [팀원 A, 팀원 B, 이민수]
related_atoms: [...]
---
```

### D.2.4 명세서

```yaml
---
title: 길드 출석 기능 명세
type: spec
priority: P1
target_milestone: MS2
---
```

---

## D.3 필수 vs 선택 필드

### D.3.1 필수 필드

| 문서 종류 | 필수 |
|---|---|
| atom | name, description, type, category, status |
| 결정 카드 | decision_id, title, type, status, created, scope |
| 회의록 | type, category, date, attendees |
| 명세서 | title, type, priority |

### D.3.2 선택 필드 (있으면 좋음)

| 문서 종류 | 선택 |
|---|---|
| atom | related, last_modified, priority |
| 결정 카드 | rationale, related_decisions, verification |
| 회의록 | related_atoms, sub_topic |
| 명세서 | target_milestone, related_atoms |

---

## D.4 Lint 자동 검사

```bash
# frontmatter_lint.py

for file in glob("**/*.md"):
    fm = parse_frontmatter(file)
    if not fm:
        warn(f"{file}: frontmatter 없음")
    
    doc_type = infer_type_from_filename(file)
    required = REQUIRED_FIELDS[doc_type]
    
    for field in required:
        if field not in fm:
            warn(f"{file}: 필수 필드 {field} 누락")
```

빌드 시 자동 실행. 위반은 alert.

---

## D.5 명명 충돌 방지

| 영역 | 방지 |
|---|---|
| atom name | 글로벌 unique |
| 결정 ID | 분기 내 unique |
| 회의 ID | 일자 + seq |
| 파일명 | 폴더 내 unique |

명명 충돌 시 자동 차단.

---

## D.6 변경 절차

### D.6.1 atom 이름 변경

```
1. 새 이름의 atom 생성
2. 기존 atom의 모든 wikilink 새 이름으로 갱신 (자동)
3. 기존 atom을 deprecated + redirect
4. 1개월 후 _archive로 이동
```

급한 이름 변경은 자료 손상 위험.

### D.6.2 frontmatter 표준 변경

```
1. 변경 사유 제안 (decision 절차)
2. 모든 기존 문서 마이그레이션 스크립트
3. 빌드 lint 갱신
4. 팀 알림
```

---

## D.7 독자 참고

본 표준은 저자의 환경. 독자는 자신의 환경에 맞춰 조정 필요. 핵심은:

| 핵심 | 이유 |
|---|---|
| 명명 일관성 | 검색·자동화 |
| Frontmatter 표준 | 도구 친화 |
| 필수·선택 분리 | 작성 부담 ↓ |
| Lint 자동 | 표준 강제 |
| 변경 절차 | 자료 보호 |
