# Changes (Blank → 최종)

> 흐름: Blank 상태 → 추가한 객체/정보 → 배치 또는 작성 판단 → 최종 결과 → Evidence → Human Review 여부

## B1DJE102 / B001 — 모듈배치도

### 1. Blank 상태 (작업 전 확인)
> 조사 방법: 원본 복사본을 AutoCAD 2027 accoreconsole `/readonly`로 열어 AutoLISP로 추출 (원본 미수정, SHA-256 동일 확인). [확인] = 추출 결과로 확인, [추정] = 해석/추정 (Human 확인 필요)

- Layer 목록/개수:
  - [확인] 42개 (기존 기재 45개 → 정정): 0, BORD, SCHM, TEXT, FENC, RCEP, ZONE, DETL, POWR, DIMM, Defpoints, GRID, BEAM, MAPS, CEN, 구조물, Plate, c-형강, BOLT, 0-TEXT, HATC, Anchor Bolt, Dimension, BasePlate, Steel, BASE, !!Steel, SS-STEEL, TITLE3, SS-PURLIN, $0$A-CURB, Anchor Bolt-Center, CENTER, Frame, Footing, STRC, DIM, 3, PLNL, 분전반+인버터+접속반, 조명분전반, e-wire
  - [확인] 모든 Layer On / Freeze·Lock 없음
  - [확인] Model 공간에 객체가 있는 Layer는 13개: 0, BORD, SCHM, TEXT, FENC, ZONE, DETL, POWR, DIMM, DIM, GRID, CEN, 구조물. 나머지는 미사용 블록 정의 내부에서만 쓰이거나 비어 있음
- Title Block 유무/내용:
  - [확인] 있음. 블록/속성이 아니라 BORD Layer에 분해된 선·TEXT로 작성 (속성 블록 0개)
  - [확인] 공사명 "인천공항 하늘정원 주차장 태양광발전설비 설치공사", 도면명 "모듈배치도", DWG NO "B-1DJ-E102-B001", SCALE 1:1,000, DATE 26.07.31, "승인용", REV A, 한빛디엔에스(주), JOB NO 2025-BEE90, DSGN/CHCK/APPR 칸 이름 3명, 도곽 격자 A–H / 1–9
  - [확인] KEY PLAN("A"~"D"구역), PARTIAL SITE PLAN 표기 있음
- Model / Layout 구성:
  - [확인] Model + 배치 탭 2개 (배치1, 배치2) (기존 기재 "배치 탭 1개" → 정정)
  - [확인] 배치1: 객체 0개, 플로터가 AutoCAD 2005 시절 경로(Default Windows System Printer.pc3)로 설정됨
  - [확인] 배치2: 뷰포트 1개. 뷰 중심 (4.32e8, 3.60e8)으로, 부지 좌표와 다름
  - [확인] 도곽은 Model 공간에 `SHEET` 블록(축척 1000, 회전 35°)으로 삽입됨. INSUNITS=4(mm), DWGCODEPAGE=ANSI_949
  - [추정] 출력은 배치 탭이 아니라 Model 공간 도곽 기준으로 하는 구성
- 기존 객체 (Base 정보):
  - [확인] BORD: 도곽/표제란/KEY PLAN (LINE 4,302, LWPOLYLINE 17,050, TEXT 69 등)
  - [확인] SCHM: LINE 10,815, LWPOLYLINE 5,857, POLYLINE 1,152, HATCH 436, SOLID 498, TEXT 517 ("전기자동차"/"E V" 각 196, "경차" 24, "BUS" 2, U/U1/U2/T1/T2/P/V 표기)
  - [확인] POWR: LINE 60,140, ARC 13,287, SPLINE 6,795, CIRCLE 860, ELLIPSE 150, LWPOLYLINE 724
  - [확인] FENC: CIRCLE 552, LINE 289, LWPOLYLINE 87, 펜스 블록 `MF-2(H2000)` 53개
  - [확인] ZONE: 점선 LWPOLYLINE 2개. 좌표 TEXT X=/Y= 4쌍(TEXT Layer)이 같은 범위에 있음
  - [확인] TEXT: 모듈 사양표(645W, 2,465×1,134×30, STC 값), 설비 규모표(A 5,472 / B 5,832 / C 5,280 / D 4,368, 합계 20,952 sheets, 13,514.04 kWp), 전기실#AB/#CD, 설치 위치 문구, 도면명·축척 표기
  - [확인] 기타: DIM 치수 7개, DETL LINE 313, 구조물 LWPOLYLINE 1개
  - [확인] 모듈 배열은 삽입된 객체 없음. 미사용 블록 정의 `삭제`(RCEP LWPOLYLINE 20,952개), `모듈4`(468개)만 남아 있음
  - [확인] 부지 밖 빈 블록 삽입: `FOUNDATION. A` 923개(CEN 913 + 0 Layer 10), `123` 360개(TEXT). 블록 정의 내부가 비어 있음 (validation.md #18 참조)
  - [확인] 방위표: `Arrow_Circle` 블록 정의만 있고 삽입 0개. 분해된 방위표 형상도 확인하지 못함 (기존 기재 "방위표" → 미확인으로 정정)
  - [추정] `삭제` 블록은 원래 모듈 배열을 묶어 둔 것 (개수 20,952 = 표의 총 모듈 수)
  - [추정] ZONE = 부지/발전구역 경계, SCHM = 주차구획·도로선
  - [추정] POWR의 성격 미판단 (약 143×389 m 범위의 호·스플라인 밀집 → 기존 시설물 또는 조경 가능성). AutoCAD에서 육안 확인 필요
- 원본 해시 / 파일 이력:
  - [확인] Blank 원본 SHA-256: B001 `25d97aaeb0f9365d64b9da41bf8b42fc9ce0b2bf4283985e9a368b689299d033` (9,511,777 bytes), B006 `7f181a9248786a712b4d3974bdfef8cbb7021a3c569a42a5137fb215e8880d0d` (7,701,384 bytes)
  - [확인] 2026-09-29 17:13 AutoCAD에서 B001을 닫을 때 저장되어 해시가 `19e701a0…`(9,517,629 bytes)로 바뀜. 원본과 비교한 결과 레이어·Layout·객체 종류별 개수·TEXT·블록 정의·도면 범위는 모두 같음 (저장 시 기록 정보만 바뀐 것으로 추정)
  - [확인] 원본(`.bak`, 조사용 복사본과 해시 동일)으로 복원해 해시 `25d97a…` 확인. 이후 AutoCAD에서는 저장하지 않음

### 2. 변경 내역
| # | Blank 상태 | 추가한 객체/정보 | 배치/작성 판단 | 최종 결과 | Evidence ID | Human Review |
|---|---|---|---|---|---|---|
| 1 | | | | | | |

### 3. 분류
- 추가한 내용:
- 유지한 Base 정보:
- 새로 판단한 내용:
- T2에서 가져온 규칙:
- T1 조건 때문에 T2와 다르게 적용한 내용:
- 근거가 부족해 반영하지 않은 내용:

### 4. 추가한 Layer
| Layer 명 | 용도 | 색상/선종류 |
|---|---|---|
| | | |

## B1DJE102 / B006 — 전체 기초 구조물 배치도

### 1. Blank 상태 (작업 전 확인)
> 조사 방법: B001과 동일. [확인] = 추출 결과로 확인, [추정] = 해석/추정 (Human 확인 필요)

- Layer 목록/개수:
  - [확인] 21개: 0, BORD, SCHM, TEXT, FENC, RCEP, ZONE, DETL, POWR, DIMM, Defpoints, GRID, MAPS, CEN, 구조물, Anchor Bolt-Center, STRC, DIM, PLNL, 조명분전반, e-wire
  - [확인] 모든 Layer On / Freeze·Lock 없음
  - [확인] Model 공간에 객체가 있는 Layer는 12개: 0, BORD, SCHM, TEXT, FENC, ZONE, DETL, POWR, DIMM, DIM, GRID, CEN (구조물 Layer는 비어 있음)
- Title Block 유무/내용:
  - [확인] 있음. B001과 같은 양식으로, BORD Layer에 분해된 선·TEXT로 작성 (속성 블록 0개)
  - [확인] 도면명 "전체 기초 구조물 배치도", DWG NO "B-1DJ-E102-B006". 공사명, SCALE 1:1,000, DATE 26.07.31, "승인용", REV A, 회사·JOB NO, 이름 3명, 격자 A–H / 1–9, KEY PLAN, PARTIAL SITE PLAN은 B001과 같음
- Model / Layout 구성:
  - [확인] Model + 배치 탭 2개 (배치1, 배치2). 배치1은 객체 0개, 배치2는 뷰포트 1개(부지 좌표와 다름). B001과 같음
  - [확인] 도곽은 Model 공간 `SHEET` 블록(축척 1000, 회전 35°). INSUNITS=4(mm), DWGCODEPAGE=ANSI_949
  - [추정] 출력은 Model 공간 도곽 기준으로 하는 구성
- 기존 객체 (Base 정보):
  - [확인] BORD, SCHM, POWR, ZONE, DETL, GRID, DIMM 객체와 좌표 TEXT X=/Y= 4쌍은 B001과 종류·개수가 같음
  - [확인] FENC: CIRCLE 552, LINE 288, LWPOLYLINE 87, ARC 4 (`MF-2(H2000)` 펜스 블록 없음)
  - [확인] TEXT: TEXT 16개(전기실#AB/#CD, A~D구역, 좌표, 도면명·축척 표기). 모듈 사양표·설비 규모표 없음
  - [확인] DIM 치수 6개 (B001은 7개)
  - [확인] 기초/구조물 객체: 보이는 객체 없음
  - [확인] 부지 밖 빈 블록 삽입: `FOUNDATION. A` 923개(CEN 913 + 0 Layer 10), `123` 360개(TEXT). 블록 정의 내부가 비어 있음 (validation.md #18 참조)
  - [확인] 블록 정의 5개뿐 (123, Arrow_Circle, ANCHOR_BOLT-PLAN-M25, FOUNDATION. A, SHEET). `Arrow_Circle` 삽입 0개
  - [추정] B001과 같은 베이스 도면에서 purge한 뒤 도면명만 바꾼 상태
  - [추정] `FOUNDATION. A`는 이름은 기초지만 내용이 없고 위치도 부지 밖이어서, 기초 배치 근거로 쓸 수 없음

### 2. 변경 내역
| # | Blank 상태 | 추가한 객체/정보 | 배치/작성 판단 | 최종 결과 | Evidence ID | Human Review |
|---|---|---|---|---|---|---|
| 1 | | | | | | |

### 3. 분류
- 추가한 내용:
- 유지한 Base 정보:
- 새로 판단한 내용:
- T2에서 가져온 규칙:
- T1 조건 때문에 T2와 다르게 적용한 내용:
- 근거가 부족해 반영하지 않은 내용:
- B001 결과와의 연계 (모듈 배치 → 구조물/기초):

### 4. 추가한 Layer
| Layer 명 | 용도 | 색상/선종류 |
|---|---|---|
| | | |
