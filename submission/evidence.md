# Evidence

> 작성 원칙
> - "T2를 참고했다"가 아니라 **어떤 T2 도면 / 어떤 설계도서 / 어떤 Engineering Knowledge**를 근거로 **어떤 판단**을 했는지 추적 가능하게 작성
> - 근거 위치는 파일 경로 + 페이지/시트/셀/레이어 등 최대한 구체적으로
> - 근거가 부족하면 억지로 채우지 말고 Confidence LOW + Human Review YES
>
> Confidence: HIGH (근거 명확, 직접 확인) / MEDIUM (근거 있으나 해석 필요) / LOW (근거 부족·추정)
> 적용 판단: 적용 / 조건부 적용 / 미적용

## 0. 조사 범위와 표기

- 팀 레포: `C:\Users\hjmo-\icn-solar-cad-agent` (commit `81cc5df`). **읽기 전용으로만 조사**했고 수정·커밋하지 않음. 아래에서 `team:` 접두어는 이 레포 기준 상대 경로.
- 팀 레포에는 `data/raw`, `data/converted`(원본 도면·DXF)가 없음. 모든 팀 레포 근거는 **2차 기록(문서·JSON·CSV)** 이며 원본 도면을 직접 열어 확인한 것이 아님.
- Blank 도면 근거: 개인 레포 `submission/drawings/dwg/B1DJE102_B001.dwg`, `B1DJE102_B006.dwg` (조사 방법은 `changes.md` 1번 참조).
- 표기
  - **[사실]**: 근거 파일에 그대로 적혀 있음
  - **[추정]**: 해석·계산·추론이며 사람 확인 필요
  - **[금지]**: T1 완성본 B001/B006 유래로 확인됨 → 근거로 사용하지 않음
  - 위치 표기에서 ★ = 원문을 직접 다시 열어 인용을 확인한 항목. ★가 없는 위치는 조사 에이전트 보고 기준(파일·행 번호는 보고대로 기재)
- 사용 허용 (사용자 지시, 2026-09-29): Blank B001 도면 안에 보이게 적혀 있는 **설비 규모표(구역별 모듈 수, 합계 20,952장)와 모듈 사양표**는 한빛DNS가 제공한 Blank의 정보이므로 근거로 사용함. 출처는 **"Blank B001 TEXT 레이어"**.
- 사용 보류 (사용자 지시): Blank B001의 숨은 블록 `삭제`(RCEP 폴리라인 20,952개)는 사용 가능 여부를 스레드에 문의 중 → **근거로 쓰지 않고 HR-EV-01로만 기록**.

## 1. Evidence 요약표

| ID | T1 도면 | 작성/변경 항목 | T2 근거 | 기타 Evidence | 적용 판단 | Confidence | Human Review |
|---|---|---|---|---|---|---|---|
| E-B001-01 | B1DJE102/B001 | 모듈 배치 기준 | T2 시방 481400절 2.4 A.1·A.3 (음영 없는 위치, 가로·세로줄 정렬, 경사각은 설계도 기준). 수치 없음 | EK 9개 중 배치 규칙 없음 | 조건부 적용 (정성 기준만) | LOW | YES (HR-EV-04) |
| E-B001-02 | B1DJE102/B001 | 모듈 수량 | T2는 도면과 수량산출서가 달랐던 사례 (13,009 vs 12,936) | Blank B001 TEXT 레이어 20,952 (A 5,472 / B 5,832 / C 5,280 / D 4,368), 수량산출서·BOQ AB 11,304 / CD 9,648 | 적용 | HIGH (합계) / MEDIUM (구역별) | YES (HR-EV-05) |
| E-B001-03 | B1DJE102/B001 | Zone 구분 | T2는 A,B-ZONE / C-ZONE 두 계통, 전기실도 Zone별 | Blank B001 KEY PLAN A~D, ZONE 레이어, 전기실#AB/#CD, 구성도 AB/CD | 조건부 적용 | MEDIUM | YES (HR-EV-06) |
| E-B001-04 | B1DJE102/B001 | 주요 간격/이격 기준 | **없음** (T2 시방에 이격 조항 자체가 없다고 명시됨) | 없음 | 미적용 | LOW | YES (HR-EV-04) |
| E-B006-01 | B1DJE102/B006 | 기초 구조물 배치 | T2 시방 481400절 구조물 조항 (재질·도금·볼트·앵커볼트 볼트캡). 배치·형식·치수 없음 | T1 시방 481400절 페이지만 대응됨 (T1 적용성 NOT_ASSESSED) | 조건부 적용 (주기·재질 문구 수준) | LOW | YES (HR-EV-07) |
| E-B006-02 | B1DJE102/B006 | 구조물/기초와 모듈 배치 관계 | **없음** | 없음 | 미적용 | LOW | YES (HR-EV-07) |
| E-B006-03 | B1DJE102/B006 | 기초 수량 | **없음** (T2 구조물·기초분야 수량산출서는 목록에만 있고 미분석) | Blank의 `FOUNDATION. A` 923개는 빈 블록·부지 밖 → 사용 불가 | 미적용 | LOW | YES (HR-EV-08) |

## 2. 항목별 상세

### 2-1. Approved Engineering Knowledge 9개 규칙

출처: ★`team:data/knowledge/approved-engineering-knowledge-v1.json` (`knowledge[*].source_candidate_snapshot`), ★`team:docs/approved-engineering-knowledge-v1.md` L39-54.

- [사실] 9개 모두 Human 결정 `APPROVE_WITH_GUARDRAILS`이며, 각 규칙의 `required_guardrails`는 반드시 지켜야 함 (문서 L102-107).
- [사실] 9개 중 **모듈 배치, 이격, Zone 경계, 구조물·기초 형상을 직접 정하는 규칙은 없음**. 모두 검토 트리거, 정합성, 데이터 해석 규칙임.
- [추정] 아래 "B001/B006 적용"은 규칙의 statement·applicability·guardrail을 읽고 내린 판단이며, 팀에서 정한 적용 결과가 아님.

| 규칙 | 내용 (statement 요약) | JSON 위치 | B001 적용 | B006 적용 | 판단 이유 |
|---|---|---|---|---|---|
| EKC-005 | 한 인버터에 직렬수가 다른 String group이 연결됐는지 탐지만 함. MISMATCH로 자동 승격 금지 | L25 | 미적용 | 미적용 | 두 도면 모두 String–인버터 구성을 정하지 않음 |
| EKC-008 | 수량/BOQ 품목이 검토 도면에 없으면 오류가 아니라 MISSING으로 기록하고 다른 sheet 확인 | L192 | 조건부 | 조건부 | 모듈·기초 품목이 이 도면에 없을 때 바로 누락으로 판단하지 말고 확대평면도·상세도 등 다른 sheet 역할을 확인해야 함 |
| EKC-017 | 수량산출서와 BOQ는 같은 item·scope·unit일 때만 수량 비교 | L368 | 조건부 | 조건부 | B001 모듈 수량 cross-check 시 사용. 모듈설치비 단위 `ea` vs `식` 차이는 WARNING (T1-KV-026) |
| EKC-018 | 접속반 채널 용량 L1/L2 검증 | L555 | 미적용 | 미적용 | 접속반 배치·채널을 정하는 도면 아님 |
| EKC-019 | 케이블 표기 차이는 허용 목록 확인 후 표기 차이로만 기록 | L773 | 미적용 | 미적용 | 케이블 표기 없음 |
| EKC-022 | 수량산출서 detail → summary → BOQ 3단계 정합성 | L978 | 조건부 | 미적용 | 수량산출서 모듈 산출식이 `5472+5832` 같은 상수 입력이라 출처 추적이 필요 (HR-EV-05) |
| EKC-024 | Excel은 수식·cached value·custom function을 구분해서 읽고 원본은 read-only | L1187 | 조건부 | 조건부 | 수량산출서(.xlsm)·BOQ(.xlsx) 값을 인용할 때 적용 |
| EKC-025 | 추출 텍스트는 렌더링/좌표로 교차확인. **UNREFERENCED/UNREACHABLE 블록 텍스트는 active evidence로 쓰지 않음** | L1350 | 적용 | 적용 | Blank TEXT 레이어 값은 렌더링 확인 필요. 미사용 블록 `삭제`·`모듈4`는 active evidence 아님 (HR-EV-01) |
| EKC-028 | 계산서 page는 설비 대수가 아님. **도면의 text hit 수·중복 라벨·미사용 블록은 설비 수량이 아님** | L1566 | 적용 | 적용 | 모듈 수·기초 수를 도면 객체나 텍스트 개수로 세지 않음. 빈 블록 `FOUNDATION. A` 923개를 기초 수량으로 쓰면 안 됨 |

- [사실] EKC-025, EKC-028 모두 승인 9개에 포함됨: `publication_provenance.human_decision = APPROVE_WITH_GUARDRAILS`, `status = APPROVED`, `additional_evidence_required = []` (`team:data/knowledge/approved-engineering-knowledge-v1.json`).
- [사실] EKC-028은 `team:docs/phase2-human-review-package-v1.md` L53에 "HUMAN_REVIEW_REQUIRED … AB zone 외 구역은 같은 교차확인 반복 필요"로 남아 있음 (진행상황 공유의 "추가 검증 필요" 항목으로 보임). 승인 자체는 유지되므로 B001에는 guardrail("drawing text hit count ≠ equipment count", 미사용 블록 제외) 범위로만 적용: **B001 모듈 수량은 도면 객체·텍스트 개수가 아니라 Blank 설비 규모표와 수량산출서·BOQ로 확인하고, 미사용 블록 `삭제`의 폴리라인 20,952개를 수량 근거로 세지 않기 위해 적용함.**

### E-B001-01 모듈 배치 기준
- T1 조건 (확인한 사실 + 근거 위치):
  - [사실] Blank B001 TEXT 레이어: 모듈 645Wp, 사이즈 2,465(W) × 1,134(H) × 30(D).
  - [사실] T1 시방 481400절 조항이 T2와 같은 문구로 대응됨: `team:workspaces/w2/t1-t2-requirement-scope-matrix.md` L75-90 (INS-002 p.199, INS-003 p.199, INS-004 p.199). 단, `t1_applicability = NOT_ASSESSED`.
- T2 근거 (도면명/번호, 위치):
  - [사실] T2 시방 481400절 2.4 A.1 "음영이 발생치 않는 부분으로 주차장 여건에 맞게 시공 … 경사각을 설계도를 기준으로" / A.3 "가로, 세로줄이 정확히 정렬되어야 한다": ★`team:data/runtime/t2-hwpx-evidence-workflow-example-v1.json` L73 (`document_structure.hwpx_spec.section_texts["Contents/section0.xml"]`).
  - [사실] T2 경사각은 NOT_COMPARABLE ("경사각은 Case 01 확인 Evidence에 없음(구조물 측면도 존재)"): ★`team:docs/case-01-requirements-v1.md` L468.
  - [사실] T2 모듈배치도 = `B1D2E102/B301` (DXF TEXT 실측, VERIFIED): ★`team:workspaces/w0/case-01-t2-drawing-validation.md` L34-45. 행×열, 방향, 테이블당 모듈 수는 추출된 기록 없음.
- Engineering Knowledge (문서/항목): 해당 규칙 없음 (2-1 참조).
- 기타 설계도서: 없음 (T1 구조물 표준상세도·구조물 일반도는 목록에만 있음: `team:data/manifests/source-inventory-t1.csv` L71-79, L87-88).
- T2 → T1 적용 논리: [추정] T1·T2 시방 481400절이 같은 문구라서 "정렬·음영 회피·경사각은 설계도 기준" 같은 정성 기준은 T1에도 적용 가능.
- T2와 다르게 적용한 점과 이유: 해당 없음 (수치 기준이 없음).
- 최종 반영값: 수치 기준 없음. 모듈 크기 2,465×1,134만 확정 입력값.
- Confidence: LOW
- Human Review: YES (HR-EV-04). 배열 형식, 모듈 방향, 경사각은 사람이 정해야 함.

### E-B001-02 모듈 수량
- T1 조건 (확인한 사실 + 근거 위치):
  - [사실] **Blank B001 TEXT 레이어**: "발전모듈수량 : 20,952 (sheets)", "더미모듈수량 : 0(sheets)", A구역 5,472 / B구역 5,832 / C구역 5,280 / D구역 4,368, "설치용량 : 모듈 645(Wp) × 20,952(sheets) = 13,514.04(kWp)".
  - [사실] 수량산출서 `03_수량산출서(전기분야).xlsm` `'산출집계'!J265 = 11304`, `J304 = 9648`; BOQ `01_공사비내역서(전기분야).xlsx` `'3-2.공종별내역서'!E294 = 11304`, `E318 = 9648`: `team:data/knowledge/t1-knowledge-candidate-validation-v1.json` T1-KV-009 evidence (L1145~). ※ 같은 KV-009 기록의 "도면" 값은 [금지] 자료 유래라서 여기서는 셀 값만 인용함.
  - [사실] 구성도 `B1DJE155/B001` AB "7,291kW ‖ 11,304", `B1DJE155/B006` CD "6,222.96kW ‖ 9,648": 같은 JSON T1-KV-010 evidence (L1173~). ※ `B1DJE155/B006`은 구성도로, 금지 대상인 `B1DJE102/B006`과 다른 도면.
  - [추정] 11,304 + 9,648 = 20,952 로 Blank 합계와 일치. 5,472 + 5,832 = 11,304 (A+B = AB), 5,280 + 4,368 = 9,648 (C+D = CD) 로 구역 구분과도 일치.
  - [추정] 645 × 20,952 = 13,514.04 kWp. 구성도 표기값 합은 7,291 + 6,222.96 = 13,513.96 이라 0.08 kW 차이 (AB 7,291.08 반올림으로 보임).
- T2 근거: [사실] T2는 도면 발전모듈 13,009 / 수량산출서 12,936 으로 달랐고 MISMATCH(설계 오류 확정 아님)로 기록됨: ★`team:docs/case-01-quantity-boq-validation-v1.md` L98, L103. → T1에서도 도면–수량산출서 대조가 필요하다는 참고 사례.
- Engineering Knowledge: EKC-017 (item·scope·unit 확인 후 비교), EKC-022 (산출식 출처 추적), EKC-028 (도면 텍스트·객체 개수 ≠ 설비 수량).
- 기타 설계도서: 수량산출서, BOQ (위 셀).
- T2 → T1 적용 논리: T2에서 도면과 수량산출서가 달랐던 사례가 있으므로, T1 B001의 수량 표기는 수량산출서·BOQ와 대조한 값을 씀.
- T2와 다르게 적용한 점과 이유: T1은 더미 0, 4구역(A~D)이라 T2(더미 35, A.B/C 2구역) 구조를 그대로 쓰지 않음.
- 최종 반영값: 합계 20,952장, 구역별 A 5,472 / B 5,832 / C 5,280 / D 4,368 (Blank B001 TEXT 레이어 기준, 이미 도면에 있음).
- Confidence: HIGH (합계·AB/CD 합계는 독립 Source 3종 일치) / MEDIUM (A/B/C/D 개별 값은 Blank 외 독립 Source 없음)
- Human Review: YES (HR-EV-05)

### E-B001-03 Zone 구분
- T1 조건:
  - [사실] Blank B001: KEY PLAN "A"~"D"구역, TEXT "A구역"~"D구역", "전기실#AB", "전기실#CD", ZONE 레이어 점선 폴리라인 2개 + 좌표 X=/Y= 4쌍 (`changes.md` B001 1번).
  - [사실] T1 구성도·전기계산서는 AB / CD 두 전기실 계통: `team:data/manifests/source-inventory-t1.csv` L98-99, L119-120 (파일명).
- T2 근거: [사실] T2는 A,B-ZONE / C-ZONE 두 계통, 인버터 AB-1, AB-2, C-1, 전기실#AB / 전기실#C: `team:workspaces/w0/case-01-t2-drawing-validation.md` L18-21, `team:docs/case-01-requirements-v1.md` L469.
- Engineering Knowledge: 해당 승인 규칙 없음. 참고로 후보 EKC-016 예외 "구역 경계가 문서마다 다르면 구역 비교 대신 합계 비교"는 NEEDS_VALIDATION / DEFER 상태라 근거로 쓰지 않음 (`team:data/knowledge/engineering-knowledge-candidates-v1.2.json` L1952).
- T2 → T1 적용 논리: [추정] "전기실 단위(AB/CD)로 구역을 묶는다"는 구성은 T2와 같은 방식.
- T2와 다르게 적용한 점과 이유: T1은 4구역(A~D) + 전기실 2개(AB, CD). T2는 3구역 + 전기실 2개(AB, C).
- 최종 반영값: A~D 4구역 (Blank에 이미 있음). 구역 경계선의 정확한 위치는 근거 없음.
- Confidence: MEDIUM
- Human Review: YES (HR-EV-06). ZONE 레이어 폴리라인 2개가 어떤 경계인지 확인 필요.

### E-B001-04 주요 간격/이격 기준
- T1 조건: [사실] 근거 없음. T1 시방 481400절도 T2와 같은 문구로만 대응되어 있음.
- T2 근거: [사실] "시방서에 없는 조건은 역추론하지 않았습니다." / "Installation: 어레이 이격거리, 배치 간격, 접지저항 값": ★`team:docs/case-01-requirements-v1.md` L228-235. 레포 전체에서 행 간격·셋백·통로·소방차로·주차면 clearance 수치를 찾지 못함 (T2 조사 결과).
- 참고로 T2 휀스 "2m 이하 간격으로 본딩"(`team:data/reviews/specialist/w3/ready-candidates-validation-v1.json` L487-492)은 접지 본딩 간격이라 모듈 이격 근거가 아님.
- 최종 반영값: 없음 (억지로 채우지 않음).
- Confidence: LOW
- Human Review: YES (HR-EV-04)

### E-B006-01 기초 구조물 배치
- T1 조건:
  - [사실] T1 시방 481400절 구조물 조항 페이지 대응 (INS-005 p.198, INS-006 p.186, INS-007 p.198, INS-008 p.201, INS-009 p.198, INS-011 p.202): `team:workspaces/w2/t1-t2-requirement-scope-matrix.md` L75-90. `t1_applicability = NOT_ASSESSED`이고 값 문구는 T2 원문으로 확인한 것.
  - [사실] 구조 관련 T1 원자료는 목록에만 있음 (내용 미추출): 구조물 표준 상세도 1~9 (`source-inventory-t1.csv` L71-79), 기타 기초 상세도 (L82), 구조물 일반도 (L87-88), 태양광 구조물 구조계산서.pdf (L121-122), 구조물·기초분야 내역서·수량산출서 (L125-131).
  - [사실] "구조계산서, 구조물·기초 분야 내역서: Candidate 범위 밖": ★`team:docs/t1-knowledge-validation-material-set-v1.md` L43.
- T2 근거:
  - [사실] T2 시방 481400절: 지내력시험·구조계산서 제출(1.1 F), 탄소구조용강·용융아연도금 KS D 8308 550 g/㎡ (1.2 G), H형강·강관·C형강·ㄱ형강 (2.4 F.1), 지지대 설치위치는 도면에 따르고 발주자 대리인과 상의 (2.4 F.3), "기초 콘크리트 앵커 볼트부분은 볼트캡을 사용" (2.4 F.8): ★`team:data/runtime/t2-hwpx-evidence-workflow-example-v1.json` L73.
  - [사실] T2 `B1D2E102` 폴더에 "전체 기초 구조물 배치도"가 있다는 제목 확인만 있음. 어느 파일(B302~B306)인지와 내용은 기록 없음: ★`team:workspaces/w0/case-01-t2-drawing-validation.md` L47.
  - [사실] T2 구조계산서는 표지만 추출됨 (B-1D2-E311-B01, "승인용"은 승인 증거 아님): `team:data/runtime/t2-hwpx-evidence-workflow-example-v1.json` L80, `team:docs/hwpx-evidence-workflow-v1.md` L51-65.
- Engineering Knowledge: 배치 규칙 없음. EKC-028 (도면 객체 개수 ≠ 설비 수량).
- T2 → T1 적용 논리: [추정] 시방 문구가 같으므로 재질·도금·앵커볼트 볼트캡 같은 주기 수준만 적용 가능.
- 최종 반영값: 기초 형식·위치·간격 근거 없음.
- Confidence: LOW
- Human Review: YES (HR-EV-07)

### E-B006-02 구조물/기초와 모듈 배치 관계
- 근거 없음. T1·T2 모두 모듈 배열과 구조물(테이블)·기초의 대응(테이블당 모듈 수, 기둥 간격 등)이 추출된 기록이 없음.
- Confidence: LOW / Human Review: YES (HR-EV-07)

### E-B006-03 기초 수량
- [사실] 근거 없음. T2 구조물·기초분야 수량산출서는 "검색하지 않았음": `team:data/reviews/specialist/wave-c/w4-candidate-v1.2-wave-c-rereview-v1.json` L98. T1도 목록에만 있음 (`source-inventory-t1.csv` L125-131).
- [사실] Blank B001/B006의 `FOUNDATION. A` 삽입 923개는 블록 정의가 비어 있고 부지 밖 좌표에 있음 (`validation.md` #18).
- [추정] EKC-028 guardrail에 따라 이 삽입 개수를 기초 수량으로 쓰면 안 됨.
- Confidence: LOW / Human Review: YES (HR-EV-08)

## 3. 확인한 사실 vs 추정

| 구분 | 내용 | 근거 |
|---|---|---|
| 사실 | Blank B001 설비 규모표: 20,952장 (A 5,472 / B 5,832 / C 5,280 / D 4,368), 더미 0, 13,514.04 kWp | Blank B001 TEXT 레이어 |
| 사실 | Blank B001 모듈 사양표: 645W, 2,465×1,134×30, STC (Voc 56.88 V, Isc 13.85 A, Vmp 48.78 V, Imp 13.22 A, 효율 23.1%) / BNPI (Voc 57.11 V, Isc 15.35 A, Vmp 48.77 V, Imp 13.65 A) | Blank B001 TEXT 레이어 |
| 사실 | 수량산출서·BOQ 모듈 AB 11,304 / CD 9,648 | T1-KV-009 evidence 셀 (`산출집계`!J265, J304 / `3-2.공종별내역서`!E294, E318) |
| 사실 | 전기계산서 STC 값이 Blank 사양표 STC 행과 같음 (56.88 / 13.85 / 48.78 / 13.22) | `team:data/knowledge/t1-knowledge-candidate-validation-v1.json` T1-KV-002 evidence 2 (전기계산서#AB p.4) |
| 사실 | 승인된 EK 9개 중 배치·이격·기초 규칙 없음 | `approved-engineering-knowledge-v1.json` |
| 사실 | T2 시방에 이격거리·배치 간격 조항 없음 | `team:docs/case-01-requirements-v1.md` L235 |
| 추정 | 11,304 + 9,648 = 20,952, A+B = AB, C+D = CD 로 구역 구분이 전기실 구분과 대응 | 계산 |
| 추정 | 구성도 kW 합 13,513.96 vs 13,514.04 차이 0.08 kW는 반올림 | 계산 |
| 추정 | T1 시방 481400절이 T2와 같은 템플릿이라 T1에도 이격 조항이 없을 것 | `t1-t2-requirement-scope-matrix` COMMON_WORDING |
| 추정 | Blank `삭제` 블록 = 원래 모듈 배열 (개수 20,952 일치) | `changes.md` B001. **근거로 쓰지 않음 (HR-EV-01)** |

## 4. 근거 부족으로 반영하지 않은 항목

| 항목 | 반영하지 않은 이유 | 필요한 추가 Evidence |
|---|---|---|
| 어레이 행×열, 모듈 방향(가로/세로), 테이블당 모듈 수 | T1·T2 모두 추출 기록 없음 | T1 구조물 표준상세도·구조물 일반도 원본, 또는 사람 지시 |
| 경사각·방위각 | T2 NOT_COMPARABLE, 시방은 "설계도 기준" | 구조계산서 또는 구조물 측면도 |
| 어레이 간 이격, 통로, 주차면·차로 clearance | 시방에 조항 없음, 수치 근거 없음 | 발주처 지침 또는 사람 판단 |
| 기초 형식·위치·간격·수량, 앵커볼트 규격·수량 | T1·T2 구조 자료 미추출 | 태양광 구조물 구조계산서, 구조물·기초분야 수량산출서, 기타 기초 상세도 |
| 구역 경계선의 정확한 위치 | ZONE 레이어 2개가 무엇인지 미확인 | 사람 확인 |
| Blank 숨은 블록 `삭제` 내용 | 사용 가능 여부 문의 중 | 스레드 답변 (HR-EV-01) |

## 5. Cross-check (계산서 / 시방서 / 수량산출서)

| 항목 | 도면 값 | 계산서 | 수량산출서 | 시방서 | 일치 여부 |
|---|---|---|---|---|---|
| 모듈 수량 합계 | 20,952 (Blank B001 TEXT) | 확인 안 됨 | 11,304 + 9,648 = 20,952 (BOQ도 같음) | 해당 없음 | 일치 |
| AB / CD 수량 | A+B 11,304 / C+D 9,648 (Blank B001 TEXT) | — | 11,304 / 9,648 | — | 일치. 단 수량산출서 산출식 `5472+5832`, `5280+4368`은 상수 입력 (HR-EV-05) |
| 모듈 출력 | 645W (Blank B001 TEXT) | 645W (전기계산서) | 645Wp | "630 W ~ 645 W" (T2 원문 기준, T1 원문 미확인) | 일치 |
| 모듈 크기 | 2,465×1,134×30 (Blank B001 TEXT) | — | — | "2465×1134 mm ± 0.5 %" (T2 원문 기준, 두께 조항 없음) | 가로·세로 일치, 두께는 비교 대상 없음 |
| STC 전기값 | 56.88 V / 13.85 A / 48.78 V / 13.22 A (Blank B001 TEXT) | 같음 (전기계산서#AB p.4) | — | — | 일치 |
| BNPI Imp | 13.65 A (Blank B001 TEXT) | — | — | — | VE 문서 14.65 A와 다름 (HR-EV-09) |
| 설치용량 | 13,514.04 kWp (Blank B001 TEXT) | — | — | — | 645 × 20,952 = 13,514.04 일치. 구성도 합 13,513.96 (반올림 차이 추정) |

## 6. 참고 금지 자료 (T1 완성본 B001/B006 유래)

아래 자료는 **근거로 사용하지 않음**. 같은 값이 Blank B001 TEXT 레이어에 있는 경우에는 Blank를 출처로 씀.

| 자료 | 위치 | 판단 |
|---|---|---|
| `B001 - 모듈배치도(완).dwg` 원본 | ★`team:data/manifests/source-inventory-t1.csv` L8, ★`team:data/manifests/source-version-evidence.csv` L66 (VERSION_CANDIDATE, "파일명에 '(완)' 표기") | [금지] |
| `B006 - 전체 기초 구조물 배치도.dwg` 원본 (파일명에 "(완)" 없음) | ★`source-inventory-t1.csv` L13 | [금지] 작성 대상과 같은 도면번호의 기존 도면이라 완성본으로 취급 (HR-EV-02, 사람 확인 완료 2026-09-29) |
| T1 통합 설계도면 PDF `인천공항 하늘정원 주차장 태양광발전설비 설치공사 설계도면.pdf` | ★`source-inventory-t1.csv` L118 | [제외] 완성된 B001/B006 sheet와 모듈 배치가 들어 있을 가능성이 높아 이번 과제에서 참고하지 않음 (HR-EV-03, 사람 결정 2026-09-29) |
| T1 확대 평면도 A~D ZONE 모듈배치 (B1DJE106 B001-B004), A~D ZONE 기초 구조물 (B015-B018) | ★`source-inventory-t1.csv` L36-39, L50-53 | [제외] 모듈 배치가 그려져 있을 가능성이 높아 이번 과제에서 참고하지 않음 (HR-EV-03, 사람 결정 2026-09-29) |
| 두 도면의 DXF 변환본 | `team:workspaces/w0/dwg-dxf-conversion-manifest-draft.csv` L5, L10 | [금지] |
| T1-KV-001/002(evidence 1)/003/009/010의 **도면 쪽 값** (STC/BNPI 사양표, 20,952, 구역 수량, 13,514.04) | `team:data/knowledge/t1-knowledge-candidate-validation-v1.json` L60-62, L991-1037, L1145-1181, ★`team:docs/t1-knowledge-candidate-validation-v1.md` L361-370 | [금지] 같은 값은 Blank B001 TEXT 레이어를 출처로 사용 |
| EKC-014/015/016/021 T1 관찰, "모듈배치도 13,514.04 kWp" 예시 | `team:docs/t1-knowledge-candidate-validation-v1.md` L184, L290, L309, L320; `team:data/knowledge/engineering-knowledge-candidates-v1.2.json` L1781 | [금지] |
| EKC-025 CAD 사양표 확인 템플릿·규칙 제안 | `team:data/runtime/ekc025-cad-source-confirmation-template-v1.json` L3, L14, L21; `team:data/runtime/ekc025-cad-critical-value-ruleset-proposal-v1.json` L33 | [금지] |
| Wave A w1/w3/w5 재검토의 B001(완) scope·handle 기록 | `team:data/reviews/specialist/wave-a/w1-…` L231-250, `w3-…` L268-319, `w5-…` L178-185, L517-540 | [금지] |
| DXF text visibility audit의 E102 B001 행 | `team:docs/dxf-text-visibility-impact-audit-v1-independent.md` L211-216, L263-268 | [금지] |
| T4 EKC-025 적용 결과 (BNPI Imp 차이) | `team:docs/t1-approved-knowledge-application-v1.md` L38 | [금지] |
| 종합보고서 "Drawing = Quantity = BOQ = 20,952"의 Drawing 값 | `team:docs/t1-comprehensive-design-validation-report-v0.1-draft.md` L233-234 | [금지] Drawing 값만 해당 |
| T5 D구역 4,368 대조 | `team:docs/t1-design-change-impact-v1.md` L26-31 | [금지] 비교 기준값이 KV-009(B001(완)) |
| material-set 문서의 B001(완) 대응표 | ★`team:docs/t1-knowledge-validation-material-set-v1.md` L12, L32 | [금지] |

※ B1DJE102/B006 유래 내용은 팀 레포 안에 인벤토리·manifest 행 외에는 없음.

### 확인했으나 근거로 쓰지 않은 자료 (참고 금지 아님)

| 자료 | 확인 결과 |
|---|---|
| ★`team:workspaces/w3/t1-b001-dxf-reproduction-summary.json` | 출처 확인 결과 `source_dwg.path`(L14)가 `B1DJE155 - 구성도/B001-전체 시스템 구성도 - AB.dwg`. 모듈배치도(B1DJE102/B001) 아님, 참고 금지 아님. 숨은 블록 DXF 재변환 확인 기록이라 B001/B006 작성에 쓸 내용 없음 |
| T1 VE 자료 (설계 VE 20260921.pdf) BNPI 값·구조물 대안 | 제안서라 승인 근거 아님 (T1-KV-025 HUMAN_REVIEW_REQUIRED) |

## 7. Human Review 항목

| ID | 내용 | 필요한 결정 |
|---|---|---|
| HR-EV-01 | Blank B001 숨은 블록 `삭제`(RCEP 폴리라인 20,952개, 미삽입). 스레드에 사용 가능 여부 문의 중. EKC-025/008 guardrail상 미사용 블록은 active evidence가 아님 | 사용 가능 여부 (답변 전까지 근거로 쓰지 않음) |
| HR-EV-02 | 팀 레포의 `B1DJE102/B006 - 전체 기초 구조물 배치도.dwg`는 파일명에 "(완)"이 없음. 작성 대상과 같은 도면이라 완성본으로 보고 제외함 | **결정 완료 (2026-09-29, 사람):** 작성 대상과 같은 도면이라 완성본으로 보고 제외 |
| HR-EV-03 | T1 통합 설계도면 PDF, B1DJE106 확대 평면도(모듈배치·기초 구조물)의 참고 가능 여부 | **결정 완료 (2026-09-29, 사람):** 모듈 배치가 그려져 있을 가능성이 높아 이번엔 참고하지 않음 (6장 [제외]) |
| HR-EV-04 | 모듈 배열 형식·방향·경사각, 어레이 이격·통로 기준 근거 없음 | 사람 지시 또는 추가 자료 |
| HR-EV-05 | A/B/C/D 구역별 수량은 Blank 외 독립 Source 없음. 수량산출서 `5472+5832`, `5280+4368`은 "도면 구역 수량표를 직접 인용한 상수"로 기록되어 있어 어느 도면에서 왔는지 불명 (`team:docs/t1-knowledge-candidate-validation-v1.md` L376) | 구역별 수량 확정 |
| HR-EV-06 | Blank ZONE 레이어 폴리라인 2개의 의미, 구역 경계선 위치 | 사람 확인 |
| HR-EV-07 | 기초 형식·위치·간격, 구조물과 모듈 배열의 관계 근거 없음 | 구조계산서·표준상세도 제공 또는 사람 지시 |
| HR-EV-08 | 기초 수량 근거 없음. Blank의 `FOUNDATION. A` 923개는 사용 불가 | 기초 수량 Source |
| HR-EV-09 | Blank 사양표 BNPI Imp 13.65 A vs VE 문서 14.65 A (`team:docs/t1-knowledge-candidate-validation-v1.md` L385, T1-KV-025) | Blank 값을 그대로 둘지 확인 |
