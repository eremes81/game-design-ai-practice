---
title: "부록 J. 약어·용어집"
appendix: J
status: v3
written: 2026-06-06
author: 이민수
version: v3
---

# 부록 J. 약어·용어집

본문에 나오는 약어와 이 책 고유 용어를 한곳에 모았습니다. 본문은 각 약어가 처음 나오는 자리에서 한 번 풀어 쓰지만, 순서대로 읽지 않거나 중간에 잊었을 때 여기서 바로 찾으시면 됩니다. 한 약어가 맥락에 따라 다른 뜻이면 둘 다 적었습니다.

이 용어집은 다음 순서로 묶었습니다. 팀 규모 등급 → 게임 기획 문서 → 게임 도메인 → 데이터·운영 → AI·도구 → UI·접근성 표준 → 파일·포맷. 찾는 약어의 성격을 먼저 떠올리면 어느 묶음에 있을지 좁혀집니다. 예를 들어 `DPS`·`TTK`는 "게임 도메인", `KPI`·`DAU`는 "데이터·운영", `atom`·`JIT`는 "AI·도구" 묶음입니다.

표기 규칙은 셋입니다. ① 일반 약어는 정식 명칭과 한국어 뜻을 함께 적었습니다. ② `atom`·`Wrapper`처럼 이 책에서만 쓰는 고유 용어는 정식 명칭 칸에 "(이 책 고유 용어)"라고 표시했습니다. ③ `PK`(전쟁 맥락의 Player Kill ↔ 데이터 맥락의 Primary Key)처럼 한 약어가 두 뜻을 갖는 경우, 본문은 처음 나올 때 어느 쪽인지 함께 적고 이 표에는 두 뜻을 모두 실었습니다.

## 팀 규모 등급

이 책은 팀 인원을 특정 숫자로 고정하지 않고 다음 세 등급으로 표기합니다. 같은 기법이라도 팀 규모에 따라 도입 깊이가 달라지기 때문입니다.

| 등급 | 인원 기준 | 설명 |
|---|---|---|
| 소규모 | \~10인 | 1인·취미 개발자부터 한 자릿수 팀까지. 대개 1\~2단계 도입으로 충분 |
| 중규모 | 10\~50인 | 이 책의 운영 사례가 나온 저자 팀이 속한 구간. 표준화·정합성 자동화의 누적 효과가 분명해지는 규모 |
| 대규모 | 100+ | 다수 파트·다수 팀. 전용 인프라와 전담 운영이 정당화되는 규모 |

본문에서 "중규모(10\~50인) 팀"처럼 등급과 인원 범위를 함께 적은 곳은 이 표를 기준으로 합니다. 1인·혼자 개발처럼 인원 자체가 의미를 갖는 자리에서는 등급 대신 정확한 수를 그대로 씁니다.

## 게임 기획 문서

| 약어 | 정식 명칭 | 뜻 |
|---|---|---|
| GDD | Game Design Document | 게임 디자인 문서. 시스템·수치·동작을 확정한 상세 사양서 |
| CDD | Concept Design Document | 컨셉 디자인 문서. GDD 이전 단계의 초기 기획서(방향·컨셉) |
| TF | TaskForce | 단기 목표를 위해 한시적으로 모은 전담팀(예: 전투 TF) |
| DD | Design Director | 디자인 디렉터. 게임의 설계 방향을 총괄하는 리드 역할 |
| RnD | Research and Development | 연구·개발. 시제품·신기법을 탐색하는 단계·조직(예: 절차적 생성 RnD) |

## 게임 도메인

| 약어 | 정식 명칭 | 뜻 |
|---|---|---|
| NPC | Non-Player Character | 플레이어가 조작하지 않는 캐릭터 |
| HUD | Heads-Up Display | 게임 화면에 겹쳐 띄우는 상태 정보(체력·미니맵 등) |
| DPS | Damage Per Second | 초당 피해량 |
| GCD | Global Cooldown | 전역 쿨다운. 한 스킬을 쓰면 모든 스킬이 잠깐 함께 잠기는 공용 대기시간 |
| TTK | Time To Kill | 대상을 처치하는 데 걸리는 시간 |
| PK | Player Kill | (전쟁·PvP 맥락) 플레이어 간 전투·살해 |
| BT | BehaviorTree | 행동 트리. NPC AI의 행동 분기를 트리로 정의한 구조 |
| FSM | Finite State Machine | 유한 상태 기계. 상태와 전이로 행동을 정의하는 모델 |
| PCG | Procedural Content Generation | 절차적 콘텐츠 생성. 룰·알고리즘으로 콘텐츠를 자동 생성 |
| VFX | Visual Effects | 시각 이펙트 |
| SFX | Sound Effects | 음향 효과 |
| VA | Voice Actor | 성우 |
| RPG / MMORPG | (Massively Multiplayer Online) Role-Playing Game | 역할수행게임 / 대규모 다중접속 온라인 RPG |
| P2W / P2E | Pay To Win / Play To Earn | 결제로 강해지는 구조 / 플레이로 수익을 얻는 구조 |
| RMT | Real Money Trading | 게임 재화의 현금 거래 |

## 데이터·운영

| 약어 | 정식 명칭 | 뜻 |
|---|---|---|
| KPI | Key Performance Indicator | 핵심 성과 지표 |
| DAU | Daily Active Users | 일일 활성 사용자 수 |
| FK | Foreign Key | 외래 키. 다른 시트의 기본키를 가리키는 컬럼 |
| PK | Primary Key | (데이터 맥락) 기본 키. 행을 고유하게 식별하는 컬럼 |
| ROI | Return on Investment | 투자 대비 효과(회수) |
| MECE | Mutually Exclusive, Collectively Exhaustive | 상호 배타·전체 포괄. 중복 없이, 빠짐없이 나누는 분류 원칙 |
| STT | Speech-to-Text | 음성을 텍스트로 변환 |
| VBA | Visual Basic for Applications | 엑셀에 내장된 매크로 언어 |
| SVN | Subversion | 파일 버전 관리 시스템 |
| telemetry | (계측 데이터) | 게임 빌드·실행에서 자동 수집하는 플레이 로그·지표(입력·전투·이탈 등). "텔레메트리"로 읽음 |

## AI·도구

| 약어 | 정식 명칭 | 뜻 |
|---|---|---|
| AI | Artificial Intelligence | 인공지능 |
| LLM | Large Language Model | 대형 언어 모델(ChatGPT·Claude 등의 바탕) |
| JIT | Just-In-Time | 필요한 순간에만 끼워 넣는 방식(이 책에서는 입력에 맞는 기억 자동 주입) |
| MCP | Model Context Protocol | AI 도구를 외부 서비스와 연동하는 표준 |
| API | Application Programming Interface | 프로그램 간 호출 규약 |
| UE | Unreal Engine | 언리얼 엔진 |
| atom | (이 책 고유 용어) | 1결정 = 1파일로 박제한 결정·규칙 카드 |
| Wrapper / Cascade / Junction | (이 책 고유 용어) | 자주 쓰는 도구 진입점 / 여러 검사를 한 번에 묶은 도구 / 본체로 연결하는 심볼릭 링크 |
| rg | ripgrep | 빠른 텍스트 검색 명령어(grep을 대체하는 CLI 도구). 코드·문서 전수 검색에 쓰임 |
| ClickUp | (태스크·이슈 트래커) | 작업·일정을 관리하는 클라우드 협업 도구. JIRA·Redmine·Linear도 같은 범주. MCP로 연동해 AI가 조회·갱신 |

## UI·접근성 표준

| 약어 | 정식 명칭 | 뜻 |
|---|---|---|
| UI / UX | User Interface / User Experience | 사용자 인터페이스 / 사용자 경험 |
| WCAG | Web Content Accessibility Guidelines | 웹 접근성 지침(명암 대비·터치 타깃 크기 등의 합격선) |
| HIG | (Apple) Human Interface Guidelines | 애플의 인터페이스 가이드라인 |
| SC | Success Criterion | WCAG의 개별 합격 기준 번호(예: SC 1.4.3) |
| pt / dp / px | point / density-independent pixel / pixel | 화면 크기 단위 |

## 파일·포맷

| 약어 | 정식 명칭 | 뜻 |
|---|---|---|
| YAML | YAML Ain't Markup Language | 사람이 읽기 쉬운 설정·데이터 표기 형식 |
| JSON | JavaScript Object Notation | 데이터 교환 표기 형식 |
| HTML / SVG | HyperText Markup Language / Scalable Vector Graphics | 웹 문서 / 벡터 그래픽 형식 |
| GLB | GL Transmission Format (Binary) | 3D 모델 바이너리 파일 형식 |

---

*PK처럼 맥락에 따라 뜻이 갈리는 약어는 본문에서 처음 나올 때 어느 쪽인지 함께 적었습니다. 헷갈리면 이 표로 돌아오시면 됩니다.*
