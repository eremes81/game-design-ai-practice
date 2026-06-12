# 20.4 MCP 프로젝트 관리 — 협업툴·문서를 LLM에 연결하다

화요일 출근 직후, 9시 12분. 나는 협업툴 보드를 열기도 전에 Claude Code 창에 한 줄을 친다.

```
이번 주 미완료 P0 태스크, 마감 임박 순으로 보여줘
```

3초쯤 멈칫하더니 답이 떴다. 협업툴을 직접 열지 않았다. 대시보드 탭을 뒤지지도, 담당자에게 메신저를 보내지도 않았다. 그런데 마감이 하루 지난 태스크 하나가 맨 위에 잡혀 있었다. 나는 그제서야 협업툴을 열어 그 카드 하나만 확인했다.

이 3초가 어떻게 만들어졌는지가 이 챕터의 전부다. 핵심은 도구를 바꾼 게 아니라는 점이다. 프로젝트 A 팀은 여전히 협업툴(본 프로젝트는 ClickUp — 태스크·일정을 관리하는 SaaS로 JIRA·Redmine·Linear도 같은 자리)을 쓴다. 협업툴이 무엇이든 이 장의 흐름은 도구 이름만 바꿔 그대로 옮겨진다. 데이터 시트도 그대로 SVN에 있고, 결정 카드도 그대로 포탈에 있다. 달라진 건 단 하나, LLM이 그 도구들을 **자기 손으로 열어 볼 수 있게** 됐다는 것이다. 그 연결의 표준이 MCP(Model Context Protocol)다.

비유하자면 안내 데스크에 신입을 한 명 더 앉히는 게 아니다. 이미 있는 자료실의 자물쇠를, LLM에게도 열어 주는 것에 가깝다. 자료실은 그대로다. 열쇠를 하나 더 깎았을 뿐이다.

---

## 20.4.1 MCP가 정확히 무엇을 연결하는가

MCP는 LLM이 외부 도구·데이터에 접근하는 표준 프로토콜이다. 표준이라는 말이 핵심이다. 협업툴용 따로, 문서용 따로, git용 따로 어댑터를 깎는 게 아니라, JSON-RPC라는 한 가지 약속 위에 각 도구가 자기를 "서버"로 노출하고, LLM은 "클라이언트"로 그 서버에 말을 건다.

구조는 세 조각이다.

<svg viewBox="0 0 760 220" xmlns="http://www.w3.org/2000/svg" font-family="sans-serif" font-size="13">
  <rect x="20" y="70" width="180" height="80" rx="8" fill="#e8f0fe" stroke="#3367d6" stroke-width="1.5"/>
  <text x="110" y="100" text-anchor="middle" font-weight="bold">MCP 클라이언트</text>
  <text x="110" y="122" text-anchor="middle">LLM / 사용자</text>
  <text x="110" y="140" text-anchor="middle" fill="#555">(Claude Code)</text>

  <rect x="300" y="70" width="160" height="80" rx="8" fill="#fef7e0" stroke="#f9a825" stroke-width="1.5"/>
  <text x="380" y="105" text-anchor="middle" font-weight="bold">프로토콜</text>
  <text x="380" y="128" text-anchor="middle">JSON-RPC</text>

  <rect x="560" y="30" width="180" height="55" rx="8" fill="#e6f4ea" stroke="#1e8e3e" stroke-width="1.5"/>
  <text x="650" y="55" text-anchor="middle" font-weight="bold">MCP 서버 — 협업툴</text>
  <text x="650" y="74" text-anchor="middle" fill="#555">태스크 검색·조회</text>

  <rect x="560" y="100" width="180" height="55" rx="8" fill="#e6f4ea" stroke="#1e8e3e" stroke-width="1.5"/>
  <text x="650" y="125" text-anchor="middle" font-weight="bold">MCP 서버 — 문서</text>
  <text x="650" y="144" text-anchor="middle" fill="#555">결정 카드·GDD 조회</text>

  <line x1="200" y1="110" x2="300" y2="110" stroke="#666" stroke-width="1.5" marker-end="url(#a)"/>
  <line x1="460" y1="100" x2="558" y2="60" stroke="#666" stroke-width="1.5" marker-end="url(#a)"/>
  <line x1="460" y1="120" x2="558" y2="128" stroke="#666" stroke-width="1.5" marker-end="url(#a)"/>
  <defs><marker id="a" markerWidth="9" markerHeight="9" refX="7" refY="3" orient="auto"><path d="M0,0 L7,3 L0,6 z" fill="#666"/></marker></defs>
</svg>

서버는 "내가 할 수 있는 일"의 목록을 노출한다. 협업툴 서버라면 `search_tasks`, `get_task`, `update_task` 같은 함수들이다. 클라이언트(LLM)는 사용자의 자연어를 받아 그중 맞는 함수를 골라 호출하고, 돌아온 JSON을 다시 자연어로 풀어 준다. 내가 "P0 태스크 보여줘"라고 했을 때 LLM이 한 일은 `search_tasks(priority=P0, status=open)`를 호출한 것뿐이다.

여기서 한 가지를 분명히 해 두자. 이 책은 MCP 서버를 손수 짜는 법을 다루지 않는다. ClickUp·JIRA·GitHub처럼 공식·커뮤니티 MCP 서버가 이미 있는 도구가 대부분이라, 기획자가 할 일은 "서버를 설치하고 연결하는 것"이지 "프로토콜을 구현하는 것"이 아니다. 프로토콜 자체는 Anthropic이 2024년 11월 공개 표준으로 발표했고, 사양은 modelcontextprotocol.io에 공개돼 있다.

---

## 20.4.2 워크드 트랜스크립트 — "이번 주 P0 보여줘"가 실제로 거치는 길

말로만 "자동으로 됩니다"라고 하면 마법처럼 들린다. 실제 한 번을 끝까지 따라가 보자. 아래는 프로젝트 A에서 협업툴 MCP를 붙인 직후, 내가 처음 돌려 본 세션을 거의 그대로 옮긴 것이다. LLM의 날것 출력을 요약 없이, 어색한 부분까지 둔다.

**① 내가 친 프롬프트 (전문)**

```
ClickUp에서 이번 주 마감인 미완료 P0 태스크를 마감 임박 순으로 정리해 줘.
각 항목에 담당자와 마감까지 남은 일수를 붙이고, 마감 지난 건 맨 위로 올려.
```

**② Claude의 날것 출력 (그대로)**

```
ClickUp 워크스페이스에서 P0·미완료·이번 주 마감 조건으로 조회했습니다.
3건이 잡혔습니다. (마감 지난 건을 맨 위로 올렸습니다.)

1. TASK_017  글로벌 쿨다운 코드 변경
   담당: teammate_a / 마감: 어제 (−1일, 지남)
2. TASK_023  voice_lint v2 적용
   담당: teammate_b / 마감: 내일 (+1일)
3. TASK_031  전투 로그 스키마 갱신
   담당: teammate_c / 마감: 금요일 (+3일)

참고: TASK_009(밸런스 테이블 검수)도 P0로 보이는데,
status가 'in review'라 '미완료'에 넣어야 할지 애매했습니다.
포함하지 않았습니다 — 필요하면 기준을 알려 주세요.
```

여기서 LLM이 스스로 멈춘 지점에 주목하자. `TASK_009`는 'in review' 상태였고, 그게 "미완료"인지 LLM이 단정하지 않고 사람에게 되물었다. MCP는 데이터를 정확히 가져오지만, "in review를 미완료로 칠지"는 팀의 정의에 달린 문제다. 이걸 LLM이 임의로 판단했다면 그게 오히려 사고다.

**③ 내가 한 검증·거부**

나는 협업툴을 열어 TASK_017 카드 하나만 확인했다. 마감이 정말 지났다. 그런데 TASK_009는 우리 팀 기준으로 'in review'도 미완료에 넣는다. LLM의 분류가 우리 규칙과 달랐다. 그래서 거부하고 기준을 다시 줬다.

**④ 재요청**

```
우리 팀은 'in review'도 미완료로 친다. 그 기준으로 다시 정리해 줘.
앞으로도 'in review' = 미완료로 간주해.
```

이후 출력에서 TASK_009가 2번 자리에 들어왔다. 마지막 문장("앞으로도 \~ 간주해")은 이 세션에만 적용된다. 매번 같은 규칙을 반복해 주기 싫다면, 이 정의를 `team_memory`의 `shared` 슬롯에 atom으로 입력해 두면 다음 세션부터 LLM이 알아서 적용한다(§20.1·§20.2 참조).

이 한 번의 왕복이 보여 주는 건 분명하다. MCP는 **정보를 정확히 가져오는 도구**이지, **판단을 대신하는 도구가 아니다.** 데이터는 자동이고 정의는 사람이 준다. 그 경계를 흐리는 순간 자동화는 사고로 바뀐다.

---

## 20.4.3 다섯 가지 활용 패턴

협업툴 조회 하나만으로는 "검색 좀 편해진 것" 이상이 안 된다. MCP가 협업 시스템이 되는 건, 도구 여러 개를 한 흐름으로 엮을 때다. 프로젝트 A에서 실제로 돌리는 다섯 패턴을 흐름으로 본다.

<svg viewBox="0 0 800 400" xmlns="http://www.w3.org/2000/svg" font-family="sans-serif" font-size="11">
  <defs><marker id="mcpar" markerWidth="9" markerHeight="9" refX="7" refY="3" orient="auto"><path d="M0,0 L7,3 L0,6 z" fill="#888"/></marker></defs>
  <text x="400" y="20" text-anchor="middle" font-size="14" font-weight="bold">MCP 다섯 활용 패턴 — 각 패턴은 독립된 한 흐름</text>
  <text x="400" y="38" text-anchor="middle" font-size="10" fill="#666">왼쪽 색 블록이 패턴, 오른쪽 흰 박스가 그 패턴이 밟는 단계(좌→우)</text>

  <!-- 패턴 1 자동 보고서 -->
  <rect x="8" y="52" width="118" height="42" rx="6" fill="#e3f2fd" stroke="#1976d2" stroke-width="1.8"/>
  <text x="67" y="70" text-anchor="middle" font-weight="bold" fill="#1565c0">패턴 1</text>
  <text x="67" y="85" text-anchor="middle" font-size="10" fill="#1565c0">자동 보고서</text>
  <rect x="138" y="53" width="118" height="40" rx="4" fill="#fff" stroke="#1976d2"/>
  <text x="197" y="69" text-anchor="middle" font-size="10">매일 09시</text>
  <text x="197" y="83" text-anchor="middle" font-size="10">스케줄러 트리거</text>
  <line x1="256" y1="73" x2="266" y2="73" stroke="#888" stroke-width="1.3" marker-end="url(#mcpar)"/>
  <rect x="268" y="53" width="118" height="40" rx="4" fill="#fff" stroke="#1976d2"/>
  <text x="327" y="69" text-anchor="middle" font-size="10">협업툴·git·</text>
  <text x="327" y="83" text-anchor="middle" font-size="10">대시보드 조회</text>
  <line x1="386" y1="73" x2="396" y2="73" stroke="#888" stroke-width="1.3" marker-end="url(#mcpar)"/>
  <rect x="398" y="53" width="118" height="40" rx="4" fill="#fff" stroke="#1976d2"/>
  <text x="457" y="76" text-anchor="middle" font-size="10">LLM 보고서 합성</text>
  <line x1="516" y1="73" x2="526" y2="73" stroke="#888" stroke-width="1.3" marker-end="url(#mcpar)"/>
  <rect x="528" y="53" width="118" height="40" rx="4" fill="#fff" stroke="#1976d2"/>
  <text x="587" y="76" text-anchor="middle" font-size="10">포탈/메신저 발송</text>

  <!-- 패턴 2 결정→태스크 -->
  <rect x="8" y="120" width="118" height="42" rx="6" fill="#e8f5e9" stroke="#388e3c" stroke-width="1.8"/>
  <text x="67" y="138" text-anchor="middle" font-weight="bold" fill="#2e7d32">패턴 2</text>
  <text x="67" y="153" text-anchor="middle" font-size="10" fill="#2e7d32">결정 → 태스크</text>
  <rect x="138" y="121" width="118" height="40" rx="4" fill="#fff" stroke="#388e3c"/>
  <text x="197" y="137" text-anchor="middle" font-size="10">결정 카드 등록</text>
  <text x="197" y="151" text-anchor="middle" font-size="9">proposal P####</text>
  <line x1="256" y1="141" x2="266" y2="141" stroke="#888" stroke-width="1.3" marker-end="url(#mcpar)"/>
  <rect x="268" y="121" width="118" height="40" rx="4" fill="#fff" stroke="#388e3c"/>
  <text x="327" y="137" text-anchor="middle" font-size="10">협업툴에</text>
  <text x="327" y="151" text-anchor="middle" font-size="10">태스크 생성</text>
  <line x1="386" y1="141" x2="396" y2="141" stroke="#888" stroke-width="1.3" marker-end="url(#mcpar)"/>
  <rect x="398" y="121" width="118" height="40" rx="4" fill="#fff" stroke="#388e3c"/>
  <text x="457" y="137" text-anchor="middle" font-size="10">담당자·마감</text>
  <text x="457" y="151" text-anchor="middle" font-size="10">자동 설정</text>

  <!-- 패턴 3 태스크→카드 -->
  <rect x="8" y="188" width="118" height="42" rx="6" fill="#fff8e1" stroke="#f9a825" stroke-width="1.8"/>
  <text x="67" y="206" text-anchor="middle" font-weight="bold" fill="#e65100">패턴 3</text>
  <text x="67" y="221" text-anchor="middle" font-size="9" fill="#e65100">태스크→카드(역방향)</text>
  <rect x="138" y="189" width="118" height="40" rx="4" fill="#fff" stroke="#f9a825"/>
  <text x="197" y="205" text-anchor="middle" font-size="10">협업툴</text>
  <text x="197" y="219" text-anchor="middle" font-size="10">태스크 완료</text>
  <line x1="256" y1="209" x2="266" y2="209" stroke="#888" stroke-width="1.3" marker-end="url(#mcpar)"/>
  <rect x="268" y="189" width="118" height="40" rx="4" fill="#fff" stroke="#f9a825"/>
  <text x="327" y="205" text-anchor="middle" font-size="10">결정 카드</text>
  <text x="327" y="219" text-anchor="middle" font-size="9">execution_log 갱신</text>

  <!-- 패턴 4 진행률 분석 -->
  <rect x="8" y="256" width="118" height="42" rx="6" fill="#f3e5f5" stroke="#7b1fa2" stroke-width="1.8"/>
  <text x="67" y="274" text-anchor="middle" font-weight="bold" fill="#6a1b9a">패턴 4</text>
  <text x="67" y="289" text-anchor="middle" font-size="10" fill="#6a1b9a">진행률 분석</text>
  <rect x="138" y="257" width="118" height="40" rx="4" fill="#fff" stroke="#7b1fa2"/>
  <text x="197" y="273" text-anchor="middle" font-size="10">분기 전체</text>
  <text x="197" y="287" text-anchor="middle" font-size="10">태스크 조회</text>
  <line x1="256" y1="277" x2="266" y2="277" stroke="#888" stroke-width="1.3" marker-end="url(#mcpar)"/>
  <rect x="268" y="257" width="118" height="40" rx="4" fill="#fff" stroke="#7b1fa2"/>
  <text x="327" y="273" text-anchor="middle" font-size="10">LLM 지연</text>
  <text x="327" y="287" text-anchor="middle" font-size="10">패턴 분석</text>
  <line x1="386" y1="277" x2="396" y2="277" stroke="#888" stroke-width="1.3" marker-end="url(#mcpar)"/>
  <rect x="398" y="257" width="118" height="40" rx="4" fill="#fff" stroke="#7b1fa2"/>
  <text x="457" y="280" text-anchor="middle" font-size="10">분기 회고 입력</text>

  <!-- 패턴 5 1:1 사전 자료 -->
  <rect x="8" y="324" width="118" height="42" rx="6" fill="#fff3e0" stroke="#e64a19" stroke-width="1.8"/>
  <text x="67" y="342" text-anchor="middle" font-weight="bold" fill="#d84315">패턴 5</text>
  <text x="67" y="357" text-anchor="middle" font-size="10" fill="#d84315">1:1 사전 자료</text>
  <rect x="138" y="325" width="118" height="40" rx="4" fill="#fff" stroke="#e64a19"/>
  <text x="197" y="348" text-anchor="middle" font-size="10">1:1 미팅 5분 전</text>
  <line x1="256" y1="345" x2="266" y2="345" stroke="#888" stroke-width="1.3" marker-end="url(#mcpar)"/>
  <rect x="268" y="325" width="118" height="40" rx="4" fill="#fff" stroke="#e64a19"/>
  <text x="327" y="341" text-anchor="middle" font-size="9">멤버 태스크 +</text>
  <text x="327" y="355" text-anchor="middle" font-size="9">team_memory·활동</text>
  <line x1="386" y1="345" x2="396" y2="345" stroke="#888" stroke-width="1.3" marker-end="url(#mcpar)"/>
  <rect x="398" y="325" width="118" height="40" rx="4" fill="#fff" stroke="#e64a19"/>
  <text x="457" y="348" text-anchor="middle" font-size="10">사전 요약 자동 생성</text>
</svg>

**패턴 1 — 자동 보고서.** 매일 아침 9시, 스케줄러가 트리거를 던지면 LLM이 협업툴 태스크 상태·git 커밋·대시보드 지표를 한꺼번에 조회해 일일 보고서를 쓴다. 발송처는 포탈 또는 팀 메신저다. 여기서 "포탈"은 §20.3에서 다룬 사내 포탈웹을 말한다. `server.py`(FastAPI)가 항상 떠 있고, Claude가 작성한 `View_*.html`이 그 위에서 동작하므로, 보고서도 포탈의 한 페이지로 자연스럽게 얹힌다.

**패턴 2 — 결정 → 태스크 자동 생성.** 결정 카드(`proposal P####`)를 등록하면, 카드의 implementation·verification 항목이 그대로 협업툴 태스크가 된다. 담당자와 마감까지 자동으로 입력된다. 회의에서 "그럼 이렇게 하기로"라고 정한 게, 손을 거치지 않고 보드의 카드로 떨어진다.

**패턴 3 — 태스크 → 결정 카드 역참조.** 패턴 2의 반대 방향이다. 협업툴 태스크가 완료되면 MCP가 원래 결정 카드의 `execution_log`를 갱신한다. "이 결정이 실제로 실행됐는가"가 자동으로 추적된다. 결정과 실행이 양방향으로 묶인다(그림의 점선).

**패턴 4 — 진행률 분석.** 분기 말, 그 분기의 모든 태스크를 한 번에 끌어와 지연 패턴을 분석한다. "어떤 종류의 태스크가 반복적으로 미뤄지는가"가 회고의 입력이 된다.

**패턴 5 — 1:1 사전 자료.** 1:1 미팅 5분 전, 해당 멤버의 협업툴 태스크·`team_memory` 슬롯·최근 활동을 합성해 사전 요약을 만든다. 1:1이 "지난번에 뭐 하고 있었죠?"로 5분을 까먹는 대신 본론부터 시작된다.

다섯 패턴의 공통점은 하나다. **사람 손에 남는 반복 작업을 줄이는 자리에서만 값이 회수된다.** 멋있어 보이려고 붙이는 패턴은 운영 부담만 늘린다.

---

## 20.4.4 단계적 도입 — 한 번에 다 붙이지 마라

MCP 서버 다섯 개를 첫날에 다 연결하는 건 가장 흔한 실패다. 순서가 있다.

| 단계 | 무엇을 | 기간 감각 |
|---|---|---|
| 1 | MCP 서버 1개 설치 (ClickUp 또는 JIRA) | 1\~2일 |
| 2 | 패턴 1개 시범 (자동 보고서) | 약 1주 |
| 3 | 5개 패턴 운영 | 1\~2개월 |
| 4 | 자체 MCP 서버 개발 (특수 도구 필요 시) | 1\~3개월 |

위 기간은 프로젝트 A의 중규모(10\~50인) 팀 기준 저자 추정이며 미검증이다. 팀 규모·도구 친숙도에 따라 달라진다. 분명한 건 **대부분의 팀은 1\~3단계로 충분하다**는 것이다. 4단계(자체 서버 개발)는 시중에 MCP 서버가 없는 특수 사내 도구를 꼭 붙여야 할 때만 간다. 거기까지 가지 않아도 효과의 대부분은 회수된다.

JIRA를 따로 언급할 이유가 있다. ClickUp이 팀 내부 보드라면, JIRA는 퍼블리셔·외주 같은 **외부 조직과 공유하는** 도구인 경우가 많다. JIRA MCP를 붙이면 외주 보드의 진행률을 매주 회의 전에 자동으로 끌어와, 지연 의심 태스크를 미리 추려 둘 수 있다. 회의가 "현황 공유"가 아니라 "결정"부터 시작된다. 단, 외부 공유 도구일수록 다음 절의 권한·유출 함정이 더 무겁게 걸린다.

---

## 20.4.5 함정 네 가지 — MCP가 양날인 이유

MCP는 LLM에게 도구를 쥐여 주는 일이다. 손에 쥔 게 칼이면 베일 수도 있다.

**함정 1 — 권한 사고.** LLM이 write 권한까지 들고 있으면 의도하지 않은 변경이 일어난다. "정리해 줘"라는 한마디에 태스크 상태를 무더기로 바꿔 버리는 식이다. 처방은 명확하다. **MCP 서버는 read-only로 시작한다.** write는 패턴 2·3처럼 꼭 필요한 곳에만, 그것도 실행 전 확인 게이트를 두고 연다. 앞의 트랜스크립트에서 LLM이 'in review' 분류를 사람에게 되물은 것도 같은 정신이다 — 애매하면 멈춘다.

**함정 2 — 데이터 유출.** MCP로 끌어온 회사 데이터가 외부 LLM API로 전송된다. 밸런스 수치, 미공개 콘텐츠, 매출 지표가 그대로 흘러갈 수 있다. 처방은 민감 데이터에 한해 자체 호스팅 LLM을 쓰거나, MCP 서버 단에서 placeholder로 치환해 내보내는 것이다(이 책 전반의 IP 보호 원칙과 같다).

**함정 3 — 의존성 폭증.** MCP 서버 5개를 critical 경로에 물려 두면, 한 곳이 죽을 때 아침 보고서 전체가 멈춘다. 처방은 핵심 1\~2개만 critical로 두고 나머지는 보조로 분리하는 것이다. 보조 서버가 죽으면 그 항목만 비고, 보고서 자체는 나온다.

**함정 4 — API 비용 폭증.** MCP 호출 한 번이 LLM 토큰과 외부 API 호출을 동시에 태운다. 자동 보고서를 5분마다 돌리면 비용이 조용히 불어난다. 처방은 호출 빈도에 cap을 걸고, 자주 바뀌지 않는 조회 결과는 캐싱하는 것이다.

네 함정을 한 줄로 묶으면, MCP의 안전한 자리는 **"read-only로 시작해, 핵심만 critical로 두고, 민감 데이터는 거르고, 호출에 상한을 건다"**이다.

---

## 20.4.6 효과 — 시간이 어디서 회수되는가

프로젝트 A에서 MCP 운영 전후로 체감한 변화다. 아래 시간 수치는 저자의 경험적 추정(미검증)이며, 절대값이 아니라 **방향과 비율**로 읽기 바란다.

| 항목 | MCP 부재 | MCP 운영 | 방향 |
|---|---|---|---|
| 일일 보고 정보 종합 | 수동 30\~60분 | 자동 \~5분 | 크게 단축 |
| 도구 간 정보 동기화 | 사람 수작업 | 자동 | 수작업 제거 |
| 1:1 사전 준비 | 10\~15분 | 자동 요약 \~3분 | 단축 |
| 외주 진행률 파악 | 회의로만 | 실시간 조회 | 상시화 |
| 결정 ↔ 태스크 연결 | 수작업 | 양방향 자동 | 누락 방지 |

가장 큰 회수는 "정보를 모으는 시간"에서 난다. 결정·판단은 여전히 사람의 일이다. MCP가 줄여 주는 건 그 앞단, 흩어진 도구를 뒤져 한자리에 모으는 단순노동이다. 이 챕터 첫머리의 3초가 정확히 그 자리다.

---

## 20.4.7 20부를 닫으며

20부는 팀 협업 시스템을 네 층으로 쌓았다.

| 장 | 핵심 |
|---|---|
| 20.1 | atom 운영 — 카테고리 분류, 분기 정리 |
| 20.2 | 팀원 메모리 — `team_memory` 5인 슬롯(leeminsoo·팀원 A/b/c·shared), 공유 vs 개인 분리 |
| 20.3 | 포탈웹 — `server.py`(FastAPI)·`build_index.py`·nginx·nssm으로 상시 가동, `View_*.html` 동작 |
| 20.4 | MCP — 5패턴·단계적 도입·권한 우선 |

네 장은 따로 노는 도구가 아니라 한 몸이다. 포탈(20.3)은 보고서가 얹히는 자리고, atom·메모리(20.1·20.2)는 LLM이 'in review = 미완료' 같은 팀 정의를 기억하는 자리며, MCP(20.4)는 그 모두를 협업툴·문서와 연결하는 배선이다. 어느 하나만 떼어 놓으면 나머지의 값도 절반으로 준다.

다음 부에서는 거버넌스와 운영을 다룬다. 도구를 이만큼 붙였을 때 따라오는 안전성·비용·저작권·윤리의 문제를, 이번 챕터의 함정들을 팀 차원의 규칙으로 끌어올려 정리한다.

---

### 이 챕터의 핵심 메시지

- MCP는 도구를 바꾸지 않고 LLM에게 기존 도구의 열쇠를 깎아 주는 표준이다.
- 데이터는 MCP가 가져오고 정의·판단은 사람이 준다 — 그 경계가 안전선이다.
- read-only로 시작해 핵심만 critical로 두면 자동화가 사고로 안 번진다.

---

## 20.4.8 따라 하기 — ClickUp MCP 첫 연결

**setup**
1. ClickUp MCP 서버(공식 또는 커뮤니티)를 설치하고, ClickUp API 토큰을 발급하세요.
2. Claude Code 설정에 MCP 서버를 등록하되 **read-only 스코프로만** 시작합니다.
3. 워크스페이스 ID를 확인해 조회 범위를 자기 보드로 제한합니다.

**prompt**
```
ClickUp에서 이번 주 마감인 미완료 P0 태스크를 마감 임박 순으로 정리해 줘.
담당자와 마감까지 남은 일수를 붙이고, 마감 지난 건 맨 위로.
```

**verify**
1. 출력된 태스크 중 1건을 ClickUp에서 직접 열어 마감·담당자가 맞는지 대조하세요.
2. LLM이 애매한 항목을 스스로 되물었는지 봅니다 — 되묻지 않고 단정했다면 분류 기준을 명시해 다시 시킵니다.
3. 자주 쓰는 정의('in review=미완료' 등)는 `team_memory`의 `shared`에 atom으로 입력해 다음 세션에 자동 적용되게 합니다.

### 1인 축소판

팀도 협업툴도 없는 1인 개발자라면, MCP의 첫 대상은 **GitHub와 로컬 문서**입니다. GitHub MCP를 read-only로 붙여 "이번 주 안 닫힌 이슈, 오래된 순으로" 같은 조회부터 시작하고, 결정 카드 대신 로컬 `decisions/` 폴더의 마크다운을 문서 MCP로 조회하세요. 자동 보고서(패턴 1)는 그대로 적용됩니다 — 발송처만 팀 메신저 대신 자기 메모 파일로 바꾸면 됩니다. 권한·비용 함정은 1인이어도 똑같이 걸리니, read-only 시작과 호출 cap은 처음부터 지키는 게 좋습니다.
