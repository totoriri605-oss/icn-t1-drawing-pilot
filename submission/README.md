# T1 Drawing Generation Pilot - Phase 1 Submission

## 1. 제출자
- 이름:
- GitHub Repository:
- Branch: task/t1-drawing-pilot-phase1-<이름>-20260929
- 제출 Commit SHA:

## 2. 사용 환경
- 사용 AI 모델: Claude Opus 5.5
- 모델 버전/명칭: Claude Opus 5.5 (claude-opus-5-5)
- 실행 도구: Claude Code v2.1.281 (VS Code 터미널)
- IDE: VS Code
- CAD Tool: Autodesk AutoCAD
- AutoCAD Version: AutoCAD 2027 (체험판, 비상업적)
- 기타 사용 도구: AutoCAD 2027 accoreconsole (`/readonly`, 도면 복사본에서 AutoLISP로 레이어·Layout·객체 추출), Claude Code 조사용 하위 에이전트 2개 (팀 레포 T1/T2 자료 조사, 읽기 전용)

## 3. 작업 시간
- 작업 시작: 2026-09-29 15:30
- 작업 종료: 2026-09-29 __:__
- 총 작업 시간:
- 자료 확인 시간:
- 프롬프트 작성/수정 시간:
- AI 실행 및 검토 시간:
- CAD 직접 수정 시간:
- AutoCAD 검증 시간:
- 최종 검증/정리 시간:
- 프롬프트 주요 수정 횟수:
- 재작업 횟수:

### 3-1. AI 작업 / 사람 작업 구분
| 작업 | 수행 주체 (AI / 사람 / AI+사람 검토) | 시간 | 비고 |
|---|---|---|---|
| 자료 확인 | AI+사람 검토 | | Blank 도면 추출·팀 레포 조사는 AI, 결과 확인·사용 허용/보류 결정은 사람 |
| 설계값 도출 | | | 아직 시작 전 |
| B001 작성 | | | 아직 시작 전 |
| B006 작성 | | | 아직 시작 전 |
| AutoCAD 검증 | AI+사람 | | Blank 상태 추출은 AI (accoreconsole), ZOOM E 확인은 사람 |
| 문서 작성 | AI (사람 지시·검토) | | changes.md, validation.md, evidence.md, README.md |

- 사람 직접 작업 시간 합계:
- AI 활용 시간 합계:

### 3-2. 작업 로그 (진행하면서 기록)
> AI 작업 시각은 파일 생성·수정 시각, 커밋 시각, 작업 기록 시각 기준 (분 단위)

| 시각 | 한 일 | 구분 |
|---|---|---|
| 15:30 | 레포 생성, 브랜치, 템플릿 준비 | 사람 |
| 15:50 | AutoCAD로 Blank 도면 확인, 레이어 개수 | 사람 |
| 16:09 | Blank DWG 2개를 임시 폴더에 복사하고 accoreconsole 첫 실행 (경로 인자 오류로 실패) | AI |
| 16:20 | AutoLISP로 두 도면의 레이어·Layout·객체 종류·TEXT·블록 추출 (원본 미수정) | AI |
| 16:21 | 블록 내용·레이어별 좌표 범위·뷰포트 추가 추출 | AI |
| 16:46 | 부지 밖 빈 블록(`FOUNDATION. A`, `123`) 좌표 재확인, 멈춰 있던 accoreconsole 프로세스 종료 | AI |
| 16:47 | changes.md B001/B006 "1. Blank 상태" 작성 (B001 잘못된 값 정정), validation.md #18 작성 | AI |
| 16:48 | AutoCAD ZOOM E 결과 보고 (도면이 화면 구석에 작게 표시) | 사람 |
| 16:48 | validation.md #18에 사람 확인 결과 반영, 커밋 `c8d56d3` | AI |
| 16:56 | 팀 레포(icn-solar-cad-agent) 읽기 전용 조사 시작, Approved EK 9개 규칙 추출 | AI |
| 16:57 | T2 분석 / T1 설계조건·검증 조사 에이전트 병렬 실행 | AI |
| 17:03 | `t1-b001-dxf-reproduction-summary.json` 출처 확인 (B1DJE155 구성도, 참고 금지 아님) | AI |
| 17:09 | evidence.md 작성 (참고 금지 자료 구분, Human Review 9건) | AI |
| 17:11 | README.md 사용 환경·작업 로그 작성 | AI |
| 17:12 | HR-EV-02 (B006 제외 확인), HR-EV-03 (통합 PDF·확대 평면도 참고 안 함) 결정 | 사람 |
| 17:13 | evidence.md에 결정·제외 사유 반영, 커밋·push | AI |

## 4. 대상 도면
- B1DJE102 / B001 — 모듈배치도
- B1DJE102 / B006 — 전체 기초 구조물 배치도

## 5. 사용한 근거
- T2 Reference:
- Approved Engineering Knowledge:
- T1 Fixed Conditions:
- 시방서:
- 계산서:
- 수량산출서:
- 기타 참고자료:

> 기존 T1 완성본 B001 / B006 참고 여부: 참고하지 않음 / (참고한 경우 사유 기록)

## 6. 도면별 작업 결과

### B1DJE102 / B001
- 수행 내용:
- 주요 변경/작성 내용:
- 판단 근거: (evidence.md 항목 ID 기재, 예: E-B001-01)
- Human Review Required: __건 (validation.md 참조)

### B1DJE102 / B006
- 수행 내용:
- 주요 변경/작성 내용:
- 판단 근거: (evidence.md 항목 ID 기재)
- Human Review Required: __건 (validation.md 참조)

## 7. 제출 파일
| 파일 | 경로 | 상태 |
|---|---|---|
| B001 DWG | drawings/dwg/B1DJE102_B001.dwg | |
| B006 DWG | drawings/dwg/B1DJE102_B006.dwg | |
| B001 DXF | drawings/dxf/B1DJE102_B001.dxf | |
| B006 DXF | drawings/dxf/B1DJE102_B006.dxf | |
| B001 PDF | pdf/B1DJE102_B001.pdf | |
| B006 PDF | pdf/B1DJE102_B006.pdf | |

- DXF 저장 버전: (예: AutoCAD 2018 DXF)

## 8. 특이사항
-
