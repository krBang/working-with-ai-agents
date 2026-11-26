# 예약 루틴 프롬프트 템플릿

설계 배경과 운영 규칙은 [`02_procedures/10_scheduled-routines.md`](../../02_procedures/10_scheduled-routines.md).

| 파일 | 종류 | 주기 예 | 이식성 |
|---|---|---|---|
| [`cloud-weekly-trend-scan.md`](cloud-weekly-trend-scan.md) | 클라우드 루틴 | 매주 월요일 아침 | 높음 |
| [`cloud-biweekly-failure-patterns.md`](cloud-biweekly-failure-patterns.md) | 클라우드 루틴 | 격주 | 높음 |
| [`cloud-one-off-research.md`](cloud-one-off-research.md) | 클라우드 루틴(1회) | 지정 일시 1회 | 템플릿 |
| [`local-weekly-session-retro.md`](local-weekly-session-retro.md) | 로컬 예약 작업 | 금요일 오후 | 중간 |
| [`local-weekly-knowledge-candidates.md`](local-weekly-knowledge-candidates.md) | 로컬 예약 작업 | 금요일 오후(회고 30분 뒤) | 낮음~중간 |

클라우드 루틴 세 개는 원문 프롬프트 파일 없이 **운영 기록(요약 문서)을 바탕으로 다시 쓴 골격**이다. 로컬 두 개는 실제 쓰던 예약 작업 정의를 일반화한 것이다.

## 공통 골격

```
<한 문단: 무엇을 해 달라는지, 답변 언어·말투>

## 입력(읽기만)        ← 읽을 것과 읽는 방법
## 찾을 신호 / 조사 대상  ← 목록
## 판정 기준            ← 문턱·분류·대조할 현재 상태(우리 스택·우리 가드)
## 출력                ← 경로 하나와 형식 고정, 또는 「최종 답변만」
## 금지                ← 수정·커밋·PR 금지, 가릴 정보
마지막 답변 형식          ← 파일 경로와 제목 몇 줄만
```

## 채워야 하는 자리표시자

| 자리표시자 | 넣을 것 |
|---|---|
| `<우리 스택>` | 언어·프레임워크·DB·배포 방식 등 한두 줄. 예: 「백엔드 언어 X, 관계형 DB Y, 저장 프로시저와 배치가 많은 레거시」 |
| `<우리 가드 목록>` | 지금 걸려 있는 안전장치를 사실대로. 예: 「커밋·푸시는 승인, 전체 스테이징 차단, 비밀 파일 읽기 차단, 운영 DB 접속 차단, 실행계획 사전 판정」 |
| `<우리 역할별 모델 배분>` | 조회·표준 작업·설계 등에 어떤 급의 모델을 쓰는지 |
| `<workspace>`·`<docs-vault>`·`<memory-dir>`·`<sessions-dir>` | 실제 경로 |
| `<owner>` | 문서 프론트매터의 작성자 표기 |

## 등록할 때

- 클라우드 루틴: 모델은 중간급, 도구는 웹 검색·웹 읽기·셸·파일 읽기만 허용하고 MCP는 연결하지 않는다. 1회성은 「지정 일시 1회 실행」으로 건다. 일정은 서비스가 쓰는 시간대(UTC인 경우가 많다)로 환산해 넣는다.
- 로컬 예약 작업: 정의 파일을 `~/.claude/scheduled-tasks/<id>/SKILL.md`에 둔다. 데스크톱 앱이 켜져 있어야 실행된다.
- 어느 계정·어느 세션에 걸었는지 메모리에 한 줄 적어 둔다.
