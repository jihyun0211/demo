# Daily Paper Recommendations — 2026-08-19

## 검색 정보

- **연구 기준일**: 2026-08-19 (요청된 `REQUESTED_DATE` 사용)
- **실제 검색 창**: 2026-08-19 단일 날짜 → 결과 없음 → 2026-08-13~2026-08-19 (7일) → 임상적으로 채택할 논문 부족 → 2026-07-20~2026-08-19 (30일)로 확장하여 채택
- **검색 쿼리**: `chest X-ray deep learning multi-label diagnosis generalization`

## 코호트 요약 (masked, cohort-level only)

`llm.hospital` 뷰를 조회한 결과:

- 총 272건의 스터디, 153명의 고유 환자 (환자당 평균 약 1.8건)
- 성별: 남성 136건, 여성 136건 (균형)
- 연령: 9~87세, 평균 약 51.5세
- 촬영 기관: 5개 기관(INST01~05)에 48~62건씩 비교적 고르게 분포
- 촬영 자세: PA 184건, AP 88건
- 소견 라벨(findings_label): No Finding이 145건으로 가장 많고, 이후 Infiltration(21), Atelectasis(16), Nodule(7), Fibrosis/Effusion(각 6) 순. 다중 소견이 동시에 표기된 복합 라벨(예: Effusion|Infiltration, Atelectasis|Effusion|Infiltration)도 다수 존재
- 전체 데이터는 합성 데이터(`is_synthetic = true`)로 구성됨

전반적으로 다기관, 다중 라벨, 중등도 클래스 불균형을 가진 흉부 X-ray 데이터셋이며, 기관 간 일반화와 라벨(소견) 잡음/희소성이 주요 임상 이슈로 확인되었습니다.

## 선정 논문

### 축 (Axes)

- **기관 간 일반화**: 여러 기관/코호트에서 모델 성능이 유지되는지
- **라벨 잡음**: 보고서 기반 소견 라벨의 잡음, 복합 라벨, 주석 부족 문제
- **모델 해석가능성**: 예측 근거를 임상적으로 검토 가능한 형태로 제공하는지
- **데이터 희소성**: 소수 클래스/소규모 데이터에서의 성능 확보 전략

---

### 1. CLEAR: an auditable foundation model for radiology grounded in clinical concepts
- **venue**: Nature Biomedical Engineering (2026)
- **축**: 기관 간 일반화, 모델 해석가능성
- 미국·유럽·아시아 4개 대형 코호트에서 외부검증된 개념 기반 흉부 X-ray 파운드모델. 예측을 개별 방사선학적 소견 단위로 분해해 제시.
- **근거**: 우리 코호트도 5개 기관에서 수집된 다중 라벨 데이터로, 기관 간 표현 차이와 소견 조합의 해석가능성이 실제 이슈로 확인됨.
- **한계**: 우리 데이터(272건, 5기관)는 CLEAR가 검증한 대형 다국가 코호트와 규모가 크게 달라, 소규모 데이터에서 동일 해석이 재현되는지는 확인 불가.
- **링크**: https://doi.org/10.1038/s41551-026-01741-4

### 2. Grounding Radiology Report Findings into Medical Image Segmentation (CF2Seg)
- **venue**: npj Digital Medicine (2026)
- **축**: 기관 간 일반화, 라벨 잡음
- 픽셀 단위 주석 없이 방사선 보고서 소견 텍스트만으로 흉부 X-ray 병변 분할을 학습하는 프레임워크. 분포 변화, 주석 부족, 보고서 잡음에도 안정적 성능 유지.
- **근거**: 우리 데이터는 픽셀 주석 없이 findings_label/report_text만 존재하며, 복합 소견 라벨이 흔해 라벨 잡음 문제가 실제로 존재.
- **한계**: 픽셀 단위 전문가 주석이 없어 분할 정확도나 병변 부담 일치도를 직접 재현·검증할 수 없음.
- **링크**: https://doi.org/10.1038/s41746-026-03051-0

### 3. UniMedDiff: a knowledge-enhanced diffusion model for medical image generation from clinical reports
- **venue**: npj Digital Medicine (2026)
- **축**: 라벨 잡음, 데이터 희소성
- 질환 지식 기반 확산모델로 보고서로부터 다양한 병리 흉부 X-ray를 합성, 1% 실제 데이터 증강만으로 전체 데이터 수준에 근접한 분류 성능 달성.
- **근거**: 우리 코호트는 Nodule(7건), Pneumothorax(5건) 등 소수 클래스가 존재하는 불균형 데이터이며 이미 합성 데이터를 포함하고 있어, 보고서 기반 합성이 소수 클래스 보강에 참고될 만함.
- **한계**: 우리 데이터는 전량 합성이라 실제 데이터 증강 효과가 동일하게 적용되는지 확인 불가.
- **링크**: https://doi.org/10.1038/s41746-026-03135-x

---

## 검토 안내

본 추천은 자동 검색·요약 결과이며, 임상 적용 전 반드시 담당 의료진의 검토가 필요합니다. 각 논문의 `relevance`는 코호트 수준 통계에만 근거하며 환자 단위 값은 포함하지 않습니다.
