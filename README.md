# 게임 기획 실무에서 바로 쓰는 AI·클로드 코드 활용법

> 지어낸 숫자는 한 개도 없다

[![License: CC BY-NC-SA 4.0](https://img.shields.io/badge/License-CC%20BY--NC--SA%204.0-lightgrey.svg)](LICENSE)
[![ISBN](https://img.shields.io/badge/ISBN-979--11--12--21479--9-blue.svg)](https://bookk.co.kr/bookStore/6a298be0ff49b1a6034c7703)
[![부크크에서 구매](https://img.shields.io/badge/BOOKK-%EC%A2%85%EC%9D%B4%EC%B1%85%20%EA%B5%AC%EB%A7%A4-orange.svg)](https://bookk.co.kr/bookStore/6a298be0ff49b1a6034c7703)

**🌐 번역판**: [English — AI Workflow for Game Designers](https://github.com/eremes81/game-design-ai-practice-en) · [日本語 — ゲームプランナーのための AI 実務ワークフロー](https://github.com/eremes81/game-design-ai-practice-ja)

<img src="assets/cover.png" alt="표지" width="320">

24년 차 게임 기획자이자 디자인 디렉터가, 생성형 AI(Claude Code)를 **매일의 실무**에 들이는 법을 정리한 실전 안내서입니다. 이론이나 전망이 아니라 설치·계정·요금 같은 첫 화면부터 시스템 설계·전투·내러티브·레벨·밸런스·UX·라이브 운영, 그리고 회의록을 결정으로 바꾸기·검증 게이트·비용 관리·저작권까지, 한 작업을 손으로 끝까지 따라갈 수 있게 묶었습니다.

부제 **"지어낸 숫자는 한 개도 없다"**가 이 책의 약속입니다. 본문의 모든 수치와 사례는 꾸며 낸 예시가 아니라 실제 작업에서 나온 것이며, 코드는 대부분 외부 의존성 없이 파이썬 표준 라이브러리만으로 그대로 돌아갑니다.

게임 밖에서 일하는 분께도 열려 있습니다. 회의록을 결정으로 바꾸고, 결정의 파급을 추적하고, 검증 게이트로 품질을 지키는 워크플로는 직무와 무관하게 작동합니다. 각 챕터의 '게임 밖 적용' 박스가 그 다리이고, 팀 없이 혼자 만드는 분을 위한 '1인 축소판'도 챕터마다 붙였습니다.

---

## 📖 읽기 시작

- **[서문 · 읽는 법](manuscript/_front-matter.md)** — 이 책을 어떻게 읽을지부터
- **[1.0 시작하기 전에 — 설치·계정·요금·터미널 생존키트](manuscript/part01-foundation/chapter-0-setup-survival-kit.md)** — 첫 화면부터 따라가기
- 본문의 도식은 ` ```mermaid ` 코드로 작성되어 **GitHub에서 그대로 렌더링**됩니다. 아래 목차에서 챕터를 클릭하면 바로 읽힙니다.

## 정식 출간

| 항목 | 값 |
|---|---|
| 저자 | 이민수 (Minsoo Lee) |
| 출판 | 부크크(BOOKK) · 종이책(흑백) |
| ISBN | 979-11-12-21479-9 |
| 출간일 | 2026-06-11 |
| 분량 | 876쪽 · 24부 + 부록 A\~N + 에필로그 |
| 구매 | **[부크크 서점에서 보기](https://bookk.co.kr/bookStore/6a298be0ff49b1a6034c7703)** |

종이책 구매는 위 부크크 링크에서 가능합니다. 이 저장소는 같은 책의 **한국어판 원고(마크다운 소스)**를 라이선스에 따라 공개한 것입니다.

## 전체 목차

> **24부 + 부록 A\~N + 에필로그 · 100개 챕터.** 부록은 [`manuscript/part99-appendix/`](manuscript/part99-appendix), 판권지는 [`manuscript/_colophon.md`](manuscript/_colophon.md).

### 1부 · 도입

- [1.0 시작하기 전에 — 설치·계정·요금·터미널 생존키트](manuscript/part01-foundation/chapter-0-setup-survival-kit.md)
- [1.1 게임 기획자의 Claude Code 첫 만남](manuscript/part01-foundation/chapter-1-first-encounter.md)
- [1.2 모델·토큰·하네스 — 한 작업의 토큰이 흐르는 길](manuscript/part01-foundation/chapter-2-model-token-harness.md)
- [1.3 메모리·권한·세팅 인프라](manuscript/part01-foundation/chapter-3-memory-permission-setting.md)

### 2부 · 정보 아키텍처

- [2.1 YAML 프론트매터 — 모든 문서를 데이터로](manuscript/part02-info-architecture/chapter-4-yaml-frontmatter.md)
- [2.2 페이지별 Atom — 1 문서 1 결정의 해부](manuscript/part02-info-architecture/chapter-5-page-atom.md)
- [2.3 Layer 설계 — 게임 시스템 추상화](manuscript/part02-info-architecture/chapter-6-layer-design.md)
- [2.4 온톨로지와 wikilink 그래프 — 의미 화살표를 검증한다](manuscript/part02-info-architecture/chapter-7-ontology-graph.md)

### 3부 · 시스템 기획

- [3.1 시스템 기획자의 일과 Layer 좌표](manuscript/part03-system-design/chapter-09-system-designer-and-layer.md)
- [3.2 스키마 우선 — $스키마가 데이터보다 먼저다](manuscript/part03-system-design/chapter-10-schema-first.md)
- [3.3 관계도 시각화 — 의존성을 눈으로 본다](manuscript/part03-system-design/chapter-11-relation-map.md)
- [3.4 AI 보조 시스템 설계 프롬프트 패턴](manuscript/part03-system-design/chapter-12-ai-assist-prompt-patterns.md)

### 4부 · 전투 기획

- [4.1 전투 기획자와 Layer — 타격감은 어느 칸에 들어가는가](manuscript/part04-combat-design/chapter-13-combat-designer-and-layer.md)
- [4.2 전투 Look & Feel — 손맛을 데이터로 잡는 자리](manuscript/part04-combat-design/chapter-14-look-and-feel.md)
- [4.3 콤보·캔슬·입력 큐 — 경로를 열거하고 검증한다](manuscript/part04-combat-design/chapter-15-combo-cancel-input.md)
- [4.4 AI 보조 전투 시뮬레이션·검증](manuscript/part04-combat-design/chapter-16-ai-combat-simulation.md)

### 5부 · 내러티브

- [5.1 NarrativeDocs Layer 0\~4 구조](manuscript/part05-narrative-design/chapter-1-narrative-docs-layers.md)
- [5.2 세계관 → 캐릭터 → 퀘스트 일관성 검증](manuscript/part05-narrative-design/chapter-2-consistency-verification.md)
- [5.3 AI 보조 내러티브 작성](manuscript/part05-narrative-design/chapter-3-ai-assisted-narrative.md)
- [5.4 대사·보이스 일관성](manuscript/part05-narrative-design/chapter-4-dialogue-voice-consistency.md)

### 6부 · 콘텐츠 기획

- [6.1 절차적 콘텐츠 생성과 AI — 두 축이 교차하는 한 칸](manuscript/part06-content-design/chapter-1-procedural-content-ai.md)
- [6.2 city_hunting_generator — 도시 30개를 4주에 만든다](manuscript/part06-content-design/chapter-2-city-hunting-generator.md)
- [6.3 NPC Persona와 Squad — 인형 박물관에서 작은 사회로](manuscript/part06-content-design/chapter-3-npc-persona-squad-pipeline.md)
- [6.4 콘텐츠 양산 워크플로 — 여러 generator를 한 라인으로 묶는다](manuscript/part06-content-design/chapter-4-content-production-workflow.md)

### 7부 · 레벨 디자인

- [7.1 절차적 레벨 디자인 마스터](manuscript/part07-level-design/chapter-1-procedural-level-design-master.md)
- [7.2 BehaviorTree 에디터 — 사람과 AI가 함께 BT json을 편집하고 검증하는 워크드 트랜스크립트](manuscript/part07-level-design/chapter-2-behaviortree-editor.md)
- [7.3 던전·필드 패턴 라이브러리](manuscript/part07-level-design/chapter-3-dungeon-field-pattern-library.md)

### 8부 · 밸런스

- [8.1 전투 밸런스 공식 — 결정론이라는 룰북의 자리](manuscript/part08-balance-design/chapter-1-combat-balance-formula.md)
- [8.2 경제 모델을 Machinations로 — 인플레이션을 회의 대신 시뮬로 잡는다](manuscript/part08-balance-design/chapter-2-economy-machinations.md)
- [8.3 Damage Simulator — 명세 DPS와 시뮬 산출이 갈라지던 날](manuscript/part08-balance-design/chapter-3-damage-simulator-2008.md)
- [8.4 AI 보조 밸런스 시뮬레이션](manuscript/part08-balance-design/chapter-4-ai-balance-simulation.md)
- [8.5 PvP·경쟁 밸런스 — 승률 매트릭스·매치메이킹·서버 권위](manuscript/part08-balance-design/chapter-5-pvp-competitive-balance.md)

### 9부 · UX/UI

- [9.1 HUD 스크린샷을 lint에 건다 — 시선 이탈·대비 미달을 AI가 잡는 자리](manuscript/part09-ux-ui-design/chapter-1-hud-layout.md)
- [9.2 스킬 버튼 배열 — 배치안 3개를 AI가 짜고, lint가 떨어뜨린다](manuscript/part09-ux-ui-design/chapter-2-skill-ui-button-column.md)
- [9.3 ArtGuide/06_UI 협업 — 기획자는 md로 쓰고, 아트팀은 html만 본다](manuscript/part09-ux-ui-design/chapter-3-artguide-ui-collaboration.md)

### 10부 · QA

- [10.1 정합성 검증 atom — 30개 시트의 FK를 지키는 cascade](manuscript/part10-qa-design/chapter-1-integrity-check-atoms.md)
- [10.2 결정 검증 3-layer 센서 — 사람 검수 증거의 자리](manuscript/part10-qa-design/chapter-2-decision-validation-3-layer.md)
- [10.3 알파 Gap Report — 갭을 자연어로 분류하고 사람이 우선순위를 매기다](manuscript/part10-qa-design/chapter-3-alpha-gap-report.md)

### 11부 · 캐릭터·펫·탈것

- [11.1 명명 규약과 스킬-아트 매핑](manuscript/part11-character-pet-mount/chapter-1-naming-and-skill-art-mapping.md)
- [11.2 펫·탈것 시스템 — 템플릿 1종에서 인스턴스 50종으로](manuscript/part11-character-pet-mount/chapter-2-pet-mount-system.md)

### 12부 · 아트

- [12.1 AI 아트 에셋 파이프라인 — 가역 단계에서 양산하고, 비가역 게이트 앞에서 멈춘다](manuscript/part12-art-direction/chapter-1-ai-art-asset-pipeline.md)
- [12.2 ArtGuide 7영역 (캐릭터·애니·몬스터·NPC·VFX·UI·환경)](manuscript/part12-art-direction/chapter-2-artguide-7-areas.md)
- [12.3 기획서 → 컨셉 → 인게임 자산 흐름](manuscript/part12-art-direction/chapter-3-spec-to-asset-flow.md)

### 13부 · 데이터·KPI

- [13.1 자유응답 수백 건을 토픽으로 — 클러스터링은 AI, 진단은 사람](manuscript/part13-data-kpi/chapter-1-faq-meta-game-analysis.md)
- [13.2 KPI 정의·추적 — 정의는 사람이, 이상신호 진단은 AI가](manuscript/part13-data-kpi/chapter-2-kpi-definition-tracking.md)
- [13.3 이상 지표에서 결정까지 — AI는 가설을, 사람은 결정을](manuscript/part13-data-kpi/chapter-3-data-driven-decisions.md)

### 14부 · 모바일

- [14.1 PC HUD 30종을 모바일 10종으로 — 제약을 룰북으로, 압축을 AI로](manuscript/part14-mobile-platform/chapter-1-mobile-hud-compression.md)
- [14.2 플랫폼별 차이 (iOS / Android / PC)](manuscript/part14-mobile-platform/chapter-2-platform-differences.md)
- [14.3 터치 / 마우스 인풋 디자인](manuscript/part14-mobile-platform/chapter-3-touch-mouse-input-design.md)

### 15부 · 라이브 운영

- [15.1 라이브 운영 개관 — 이벤트 후보를 AI가 조합하고, 룰북이 거르고, 사람이 고른다](manuscript/part15-live-ops/chapter-1-live-ops-overview.md)
- [15.2 이벤트·시즌 운영 — 템플릿 1장에서 변주 후보 10개를, 검수만 사람이](manuscript/part15-live-ops/chapter-2-event-season-ops.md)
- [15.3 피드백 100건을 토픽으로 — 클러스터링은 LLM에, 우선순위는 사람에](manuscript/part15-live-ops/chapter-3-user-feedback-cycle.md)

### 16부 · 커뮤니케이터

- [16.1 전투 TF 운영 — 격리된 작업공간에서 결정만 정본으로](manuscript/part16-communicator/chapter-1-taskforce-operations.md)
- [16.2 타 직군과의 협업 — 외부 요청을 3-track으로 분류하기](manuscript/part16-communicator/chapter-2-cross-job-collaboration.md)
- [16.3 한 결정, 세 가지 포장 — 직군별 산출물 framing](manuscript/part16-communicator/chapter-3-cross-team-artifact-framing.md)

### 17부 · 회의록

- [17.1 회의록은 왜 가장 큰 통증인가](manuscript/part17-meeting-notes/chapter-1-concept-and-motivation.md)
- [17.2 회의록에서 결정을 캐내는 추출 파이프라인](manuscript/part17-meeting-notes/chapter-2-extraction-pipeline.md)
- [17.3 회의 분류·캡션·동기화 — 자산이 되는 회의록의 세 축](manuscript/part17-meeting-notes/chapter-3-categories-and-sync.md)
- [17.4 회의록을 결정 데이터베이스로 — AI 자동화 5지점](manuscript/part17-meeting-notes/chapter-4-ai-meeting-automation.md)

### 18부 · 의사결정·임팩트

- [18.1 의사결정 추적 시스템](manuscript/part18-decision-impact/chapter-1-decision-tracking-system.md)
- [18.2 임팩트 전파·등급 분류](manuscript/part18-decision-impact/chapter-2-impact-propagation-classification.md)
- [18.3 결정 전후 영향 추적 워크플로 — 사전 평가에서 사후 검증까지](manuscript/part18-decision-impact/chapter-3-pre-post-tracking-workflow.md)
- [18.4 문서 영향도 grep 워크플로 — impact로 영향 범위를 뽑는다](manuscript/part18-decision-impact/chapter-4-doc-impact-grep-workflow.md)

### 19부 · 팀장·리드

- [19.1 비전을 결정의 채점표로 — decisions/ 26개를 LLM에 걸어 보다](manuscript/part19-team-lead/chapter-1-vision-and-delegation.md)
- [19.2 갈등을 분류하고 회의에서 결정을 흘리지 않는다 — 회의 리더십 AI 보조](manuscript/part19-team-lead/chapter-2-conflict-and-meeting-leadership.md)
- [19.3 AI 도입 전략과 경영진 설득 — 보수적에서 진보적으로, ROI는 가공하지 않는다](manuscript/part19-team-lead/chapter-3-ai-adoption-strategy.md)

### 20부 · 팀 협업

- [20.1 1인 DD가 5인분 협업 메모리를 운영한다 — team_memory 시스템](manuscript/part20-team-collab/chapter-1-team-memory-operations.md)
- [20.2 팀원별 메모리 — 사용자 칸과 공유 칸의 분리](manuscript/part20-team-collab/chapter-2-team-member-memory.md)
- [20.3 기획 포탈 — 팀이 브라우저로 들어오는 입구](manuscript/part20-team-collab/chapter-3-portal-web.md)
- [20.4 MCP 프로젝트 관리 — 협업툴·문서를 LLM에 연결하다](manuscript/part20-team-collab/chapter-4-mcp-project-management.md)

### 21부 · 자가 개선

- [Part 21 · 1장. 회고가 모든 것의 시작점](manuscript/part21-self-improving/chapter-1-retro-as-origin.md)
- [Part 21 · 2장. 회고 시스템과 atom 승격 — 발견을 영구 자산으로](manuscript/part21-self-improving/chapter-2-retro-system-atom-promotion.md)
- [Part 21 · 3장. self-improving 루프 닫기](manuscript/part21-self-improving/chapter-3-closing-the-loop.md)

### 22부 · 거버넌스

- [22.1 프롬프트 엔지니어링 — 게임 기획자의 작업지시서 한 장](manuscript/part22-governance/chapter-1-prompt-engineering.md)
- [22.2 자신 있게 거짓을 말하는 동료 — 환각을 검증 게이트로 막는다](manuscript/part22-governance/chapter-2-ai-safety-hallucination.md)
- [22.3 AI 비용 관리 — 토큰 예산을 코드로 지킨다](manuscript/part22-governance/chapter-3-ai-cost-management.md)
- [22.4 저작권과 윤리 — 산출물의 권리·표시·합의를 한 절차로 닫는다](manuscript/part22-governance/chapter-4-copyright-ethics.md)

### 23부 · 확장·차세대

- [Part 23 · 1장. Wrapper·Cascade·Junction 패턴](manuscript/part23-extension/chapter-1-wrapper-cascade-junction.md)
- [Part 23 · 2장. Hermes Agent 도입기](manuscript/part23-extension/chapter-2-hermes-agent.md)
- [Part 23 · 3장. 도구 큐레이션 — 안 쓰는 도구를 데이터로 잘라낸다](manuscript/part23-extension/chapter-3-tool-curation.md)
- [Part 23 · 4장. 혼자 만든 퍼즐 게임 — Critter Sort 실전기](manuscript/part23-extension/chapter-4-personal-game-dev.md)

### 24부 · 운영 노하우

- [24.1 검증 시스템 — 정합·링크·stale를 코드로 잡는다](manuscript/part24-ops-deep/chapter-1-verification-system.md)
- [24.2 Mermaid 다이어그램 자동화 — 문서가 자기 그림을 그리게 하기](manuscript/part24-ops-deep/chapter-2-mermaid-diagram-automation.md)
- [24.3 Wikilink와 문서 위계 — 연결과 분류, 검색의 두 입구](manuscript/part24-ops-deep/chapter-3-wikilink-and-hierarchy.md)
- [24.4 출처 추적·data lineage](manuscript/part24-ops-deep/chapter-4-source-tracking-data-lineage.md)

### 부록 · 에필로그

- [에필로그 — 질문창에서 게임 디자인룸으로](manuscript/part99-appendix/epilogue.md)
- [부록 A. 회사 PC 시스템 상세 인벤토리](manuscript/part99-appendix/appendix-A-company-inventory.md)
- [부록 B. 도구 차용 절차 (회사에서 개인으로 범용화하기)](manuscript/part99-appendix/appendix-B-tool-adoption-procedure.md)
- [부록 C. 권한·세팅 레퍼런스](manuscript/part99-appendix/appendix-C-permissions-settings.md)
- [부록 D. R&D 문서 명명·Frontmatter 표준](manuscript/part99-appendix/appendix-D-naming-frontmatter-standard.md)
- [부록 E. MCP 서버 카탈로그 (게임 기획 관점)](manuscript/part99-appendix/appendix-E-mcp-server-catalog.md)
- [부록 F. 사례 색인 (회사 / 개인 PC)](manuscript/part99-appendix/appendix-F-case-index.md)
- [부록 G. 운영 스크립트 사례집](manuscript/part99-appendix/appendix-G-operation-scripts.md)
- [부록 H. 과거 작업 자료 재활용](manuscript/part99-appendix/appendix-H-past-work-reuse.md)
- [부록 I. BehaviorTree 에디터 사례 (심화)](manuscript/part99-appendix/appendix-I-behaviortree-editor.md)
- [부록 J. 약어·용어집](manuscript/part99-appendix/appendix-J-glossary.md)
- [부록 K. 다른 LLM·하네스로 이식하기](manuscript/part99-appendix/appendix-K-tool-neutral-porting.md)
- [부록 L. 팀 도입 TCO·온보딩 워크시트](manuscript/part99-appendix/appendix-L-team-adoption-tco.md)
- [부록 M. 차원 벡터·임베딩 — 게임 기획자를 위한 직관](manuscript/part99-appendix/appendix-M-embedding-intuition.md)
- [부록 N. 강의용 15주 진도표·난이도 가이드](manuscript/part99-appendix/appendix-N-course-syllabus.md)

---

## 라이선스

이 저작물은 **[CC BY-NC-SA 4.0](LICENSE)** (저작자표시-비영리-동일조건변경허락)에 따라 이용할 수 있습니다.

- 비영리 목적의 공유·번역·각색은 원저자(이민수 · Minsoo Lee)와 출처를 표시하면 허용합니다.
- 상업적 이용은 저자의 별도 허락이 필요합니다.

일부 예시용 래스터 이미지 참조(예: `char_skill_ui.png`)는 원본 없이 자리 표시만 남아 깨진 이미지로 보일 수 있습니다 — 정식 출간본(PDF/종이책)에서는 해당 자리가 채워져 있습니다.

ⓒ 이민수 2026
