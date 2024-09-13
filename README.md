# Title (Please modify the title)
## Team

| ![박패캠](https://avatars.githubusercontent.com/u/156163982?v=4) | ![이패캠](https://avatars.githubusercontent.com/u/156163982?v=4) | ![최패캠](https://avatars.githubusercontent.com/u/156163982?v=4) | ![김패캠](https://avatars.githubusercontent.com/u/156163982?v=4) | ![오패캠](https://avatars.githubusercontent.com/u/156163982?v=4) |
| :--------------------------------------------------------------: | :--------------------------------------------------------------: | :--------------------------------------------------------------: | :--------------------------------------------------------------: | :--------------------------------------------------------------: |
|            [이주하](https://github.com/jl3725)             |            [김동규](https://github.com/Lumiere001)             |            [김요셉](https://github.com/sebi0334)             |            [유재현](https://github.com/hyeon3730)             |            [최수민](https://github.com/raeul0304)             |
|                            팀장, Project Manager                             |                            Evaluation and Optimization Specialist                             |                            Modeling Expert                             |                            Preprocessing Specialist                            |           Feature Engineering Specialist                                              |

## 0. Overview

### Environment
- **Operating System**: Ubuntu 20.04 (Kernel: 5.4.0-166-generic)
- **Python Version**: 3.10.13
- **CPU**: AMD Ryzen Threadripper 3970X 32-Core Processor
- **GPU**: RTX 3090
- **RAM**: 251GiB
- **DISK Space**: 1.8TB

### Requirements
- **CatBoost**
- **Scikit-learn**: 1.5.1
- **LightGBM**
- **XGBoost**
- **Optuna**: 4.0.0
- **Pandas**: 2.2.2
- **Numpy**: 1.23.5
- **Matplotlib**: 3.7.1
- **Seaborn**: 0.12.2
- **Eli5**: 0.13.0
- **FLAML**: 2.2.0
- **Tqdm**: 4.66.1

---

## 1. Competition Info

### Overview
- **대회 이름**: 아파트 가격 예측 (House Price Prediction)
- **목표**: 서울의 아파트 실거래가를 예측하는 모델 개발.
- **배경**: 아파트 가격은 아파트 자체의 가치뿐 아니라 주변 요소에 따라 큰 변동을 겪습니다. 예측 모델은 부동산 시장의 동향을 분석하고, 합리적인 가격 예측을 통해 거래를 돕습니다.
- **평가 방식**: Root Mean Squared Error (RMSE)
- **제공 데이터**:
  1. 아파트 실거래가 데이터 (국토교통부 제공)
  2. 지하철 정보 데이터 (서울시 제공)
  3. 버스 정류장 정보 데이터 (서울시 제공)
  4. 평가 데이터 (최종 검증용)

- **주요 작업**: 다양한 회귀 알고리즘(선형 회귀, 결정 트리, 랜덤 포레스트, 딥 러닝 등)을 통해 아파트 실거래가를 예측.
- **제출 형식**: CSV 파일

### Timeline
- **프로젝트 기간**: 2024년 9월 2일 (월) 10:00 ~ 9월 13일 (금) 13:00
- **팀 병합 마감일**: 2024년 9월 4일 (수) 10:00
- **팀명 컨벤션**: ML 7조
- **최종 제출 마감일**: 2024년 9월 13일 (금) 13:00

## 2. Components

### Directory

- _Insert your directory structure_

e.g.
```
├── code
│   ├── jupyter_notebooks
│   │   └── model_train.ipynb
│   └── train.py
├── docs
│   ├── pdf
│   │   └── (Template) [패스트캠퍼스] Upstage AI Lab 1기_그룹 스터디 .pptx
│   └── paper
└── input
    └── data
        ├── eval
        └── train
```

## 3. Data Description

- **Train Data**: 1,118,822 rows × 52 columns
- **Test Data**: 9,272 rows × 51 columns (target 제외)

### Dataset Overview

- **시군구**: 아파트가 위치한 시/군/구 (예: 서울특별시 강서구)
- **번지, 본번, 부번**: 아파트의 주소 정보
- **아파트명**: 아파트 이름 (예: 트윈캐슬B동)
- **전용면적(㎡)**: 아파트의 전용 면적 (예: 79.38㎡)
- **계약년월**: 거래 연도 및 월 (예: 201304)
- **계약일**: 거래가 발생한 날짜 (예: 10일)
- **층**: 아파트 층수 (예: 4층)
- **건축년도**: 아파트 건축 연도 (예: 2003년)
- **도로명**: 도로명 주소
- **좌표X, 좌표Y**: 아파트 위치의 좌표 정보
- **target**: 거래 금액 (예: 26,000)

### EDA

1. **기초 통계 분석**: 각 변수의 기초 통계 및 아파트 가격 분포 시각화.
2. **지역별 분석**: 특정 지역(강남, 강북)의 가격 차이 분석.
3. **상관관계 분석**: 전용면적, 층, 건축년도와 거래 금액 간 상관관계 분석.

**결론**:
- 전용면적, 건축년도, 층이 거래 금액에 큰 영향을 미침.
- 강남 지역 아파트가 평균적으로 더 높은 가격을 기록.

### Data Processing

1. **결측치 처리**: 결측치가 많은 변수들은 제외하거나 채움.
2. **Label Encoding**: 시군구, 아파트명 등의 카테고리형 변수에 Label Encoding 적용.
3. **스케일링**: 연속형 변수(전용면적, 층)에 대해 StandardScaler 적용.
4. **파생 변수 생성**: 전용면적을 기준으로 소형(60㎡ 이하), 중형(60~85㎡), 대형(85㎡ 이상)으로 파생 변수 생성.

---

## 4. Modeling

### Model Description

- **Model Used**: CatBoost, LightGBM, XGBoost, Random Forest 등
- **이유**: CatBoost는 범주형 데이터를 자동 처리하며 튜닝이 적어도 높은 성능을 보여줌. Optuna를 사용해 하이퍼파라미터를 최적화하여 성능을 향상시킴.

### Modeling Process

1. **Train/Validation Split**: 데이터를 80:20으로 분리하여 학습 및 검증에 사용.
2. **Hyperparameter Tuning**: Optuna로 CatBoost 모델의 하이퍼파라미터 최적화.
3. **Training**: 최적화된 파라미터로 모델 학습.
4. **Testing**: 테스트 데이터에 적용해 예측값 생성.

---

## 5. Result

### Leader Board
- **[MID]**: 15167.3152  
- **[Final]**: 12917.0588

### Presentation

- _Insert your presentaion file(pdf) link_

## etc

### Meeting Log

- _Insert your meeting log link like Notion or Google Docs_

### Reference

- _Insert related reference_
