# AutoCAD Validation

- AutoCAD Version:
- Validation Date: 2026-09-29
- 검증자:

> 결과값: PASS / WARNING / FAIL / N/A

## 1. 결과 요약

| Drawing | DWG | DXF | PDF | Notes |
|---|---|---|---|---|
| B1DJE102/B001 | | | | |
| B1DJE102/B006 | | | | |

## 2. 상세 체크리스트

| # | 확인 항목 | B001 | B006 | 비고 |
|---|---|---|---|---|
| 1 | DWG 정상 열림 | | | |
| 2 | Missing Font / SHX 경고 | | | |
| 3 | XREF 누락 | | | |
| 4 | Block / Attribute 정상 표시 | | | |
| 5 | 한글 TEXT / MTEXT 깨짐 | | | |
| 6 | Layer 상태 | | | |
| 7 | Line Type / Line Weight | | | |
| 8 | Dimension 표시 | | | |
| 9 | Hatch 표시 | | | |
| 10 | Model Space / Paper Space | | | |
| 11 | Viewport | | | |
| 12 | 축척 | | | |
| 13 | 용지 설정 | | | |
| 14 | Plot Preview | | | |
| 15 | Title Block | | | |
| 16 | 추가한 객체 위치 | | | |
| 17 | Base 객체 의도치 않은 삭제/이동 없음 | | | |
| 18 | Zoom Extents 시 비정상 외부 객체 없음 | WARNING (Blank 기준) | WARNING (Blank 기준) | [확인] 두 도면 모두 부지(X 152,904,000~153,934,000 / Y 538,272,000~539,240,000 mm) 밖에 빈 블록 삽입이 있음: `FOUNDATION. A` 913개(CEN, X −230.1e6~−229.8e6 / Y 204.3e6~204.6e6) + 10개(0 Layer, X 29.1e6~31.4e6 / Y 44.1e6~44.8e6), `123` 360개(TEXT, X −543.6e6~−543.3e6 / Y 840.6e6~840.9e6). 두 블록 정의 모두 내부가 비어 있음. [Human 확인] 2026-09-29 AutoCAD에서 ZOOM E를 직접 실행한 결과, 도면이 화면 한쪽 구석에 작게 표시됨 (부지 밖 객체 때문에 범위가 넓어짐). [추정] 원인이 위 빈 블록인지, 다른 Layer(BORD/SCHM 등)의 부지 밖 형상인지는 아직 특정하지 못함. 정리(삭제/purge) 여부는 Human Review 대상 |

## 3. DXF 검증

| 항목 | B001 | B006 | 비고 |
|---|---|---|---|
| DXF 저장 버전 | | | |
| DXF 재열기 정상 | | | |
| Font 손상 | | | |
| Block / Attribute 손상 | | | |
| Dimension / Hatch 손상 | | | |
| DWG와 주요 설계내용 동일 | | | |
| Layer 수 (DWG / DXF) | | | |

## 4. PDF 검증

| 항목 | B001 | B006 | 비고 |
|---|---|---|---|
| 용지 크기 / 축척 | | | |
| 선 굵기 / 글자 가독성 | | | |
| 잘림 / 누락 없음 | | | |

## 5. Human Review

<!-- 항목마다 복사 -->
### HR-01
- Drawing:
- Issue:
- 영향:
- 관련 Evidence ID:
- Human Review 필요 여부: YES

## 6. Human Review Required 총 건수
- B001: __건
- B006: __건
- 합계: __건
