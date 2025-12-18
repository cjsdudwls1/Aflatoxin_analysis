# Aflatoxin_analysis
DATA : "https://drive.google.com/file/d/1rbUffAgCrT_JqwrDk4ofR-i7Y4ihu5Fa/view?usp=sharing"
---
# 🦠 아플라톡신 생성 예측 및 분석 (Aflatoxin Prediction Analysis)

> **한 줄 소개:** 기상 정보와 식품 검사 데이터를 결합하여 아플라톡신 발생 위험을 예측하고, 도메인 지식 기반의 특성 공학을 통해 예측 성능을 극대화한 머신러닝 프로젝트

<br>

## 📖 개요 (Overview)
* **프로젝트 명:** 아플라톡신 생성 예측 모델링
* **개발 기간:** 202X.XX.XX ~ 202X.XX.XX (진행 중)
* **주요 목표:** * 기상 조건(온도, 습도, 일조시간 등)과 아플라톡신 발생 간의 상관관계 분석
    * 불균형 데이터(Imbalanced Data) 처리를 통한 부적합(위험) 식품 탐지 성능 향상
    * 문헌 기반 파생 변수 생성을 통한 모델 성능 개선

<br>

## 🛠 기술 스택 (Tech Stack)

| 구분 | 스택 (Stack) |
| :-- | :-- |
| **Language** | ![Python](https://img.shields.io/badge/Python-3.9+-3776AB?style=flat-square&logo=python&logoColor=white) |
| **Data Processing** | ![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat-square&logo=pandas&logoColor=white) ![NumPy](https://img.shields.io/badge/NumPy-013243?style=flat-square&logo=numpy&logoColor=white) |
| **Modeling** | ![Scikit-Learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat-square&logo=scikit-learn&logoColor=white) (Random Forest) |
| **Environment** | ![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=flat-square&logo=jupyter&logoColor=white) Google Colab |

<br>

## ✨ 주요 기능 및 분석 과정 (Key Features & Workflow)

### 1. 🌦️ 데이터 수집 및 전처리 (Preprocessing)
* **데이터 병합:** 식품 검사 데이터(LIMS)와 기상 관측 데이터(종관기상관측 ASOS) 결합
* **결측치 처리:** 일조시간 등 기상 데이터의 결측 보완 및 이상치 제거
* **인코딩:** 검사 목적(`INSPCT_PURPS_NAME`), 품목명 등 범주형 변수 One-Hot Encoding 처리

### 2. 📊 탐색적 데이터 분석 (EDA)
* **불균형 데이터 확인:** '적합' 대비 극소수인 '부적합' 데이터 비율 확인 (약 0.5%)
* **상관관계 분석:** 기상 변수와 부적합 판정 간의 연관성 시각화
* **분포 확인:** 식품 품목별, 검사 목적별 데이터 분포 파악

### 3. 🧬 도메인 지식 기반 특성 공학 (Feature Engineering)
* **문헌 기반 파생 변수 생성:** 아플라톡신 생성에 영향을 미치는 생물학적 조건 반영
    * **독소 생성 최적 온도 일수 (`optimal_temp_days_7d`):** 25~35°C 구간 지속 일수 (Ref: FAO, 2001)
    * **저습도 일수 (`low_humid_days_7d`):** 습도 60% 미만 지속 일수 (Ref: 강릉원주대, 2014)
    * **가뭄 스트레스 지수 (`drought_stress_7d`):** 연속 무강수 일수 기반 (Ref: Bowen & Hagan, 2015)

### 4. 🤖 모델링 및 성능 평가 (Modeling & Evaluation)
* **알고리즘:** Random Forest Classifier 활용 (Class Weight 조정으로 불균형 대응)
* **최적 임계값 탐색:** F1-Score를 최대화하는 확률 임계값(Threshold) 자동 탐색
* **성능 비교:** 기본 모델 vs 특성 공학 적용 모델 성능 비교
    * *Precision (정밀도):* 약 40% 향상
    * *Recall (재현율):* 약 39% 향상
    * *F1-Score:* 약 40% 향상

<br>

## 📂 폴더 구조 (Directory Structure)
```text
root/
├── 0_일조시간_생성.ipynb          # 기상 데이터(일조시간) 전처리 및 병합
├── 1_데이터_전처리+2_EDA.ipynb    # 데이터 병합, 정제 및 탐색적 분석(EDA)
├── 3_특성공학.ipynb               # 도메인 지식 기반 파생 변수 생성 및 모델 성능 비교
├── 4_모델링.ipynb                 # 최종 모델 학습 및 결과 분석
└── README.md                      # 프로젝트 설명 문서

```

## 🚀 실행 방법 (Getting Started)

1. **환경 설정**
* Python 3.9 이상 필요
* 필수 라이브러리 설치:
```bash
pip install pandas numpy scikit-learn matplotlib seaborn

```




2. **데이터 준비**
* Google Drive 마운트 필요 (경로: `/content/drive/MyDrive/...`)
* 기상 데이터 및 LIMS 데이터 파일 위치 확인


3. **노트북 실행 순서**
1. `0_일조시간_생성.ipynb`: 기상 데이터셋 준비
2. `1_데이터_전처리+2_EDA.ipynb`: 전체 데이터셋 병합 및 EDA 수행
3. `3_특성공학.ipynb`: 핵심 파생 변수 생성 및 효용성 검증
4. `4_모델링.ipynb`: 최종 예측 모델 학습



## 📈 분석 결과 요약 (Results)

| Metric | Basic Model | Enhanced Model | Improvement |
| --- | --- | --- | --- |
| **Accuracy** | 0.7262 | **0.7304** | +0.57% |
| **Precision** | 0.0092 | **0.0129** | **+40.68%** |
| **Recall** | 0.2671 | **0.3727** | **+39.53%** |
| **F1-Score** | 0.0178 | **0.0250** | **+40.64%** |
| **ROC-AUC** | 0.4982 | **0.5496** | +10.32% |

> *도메인 지식을 활용한 특성 공학이 단순 데이터 학습보다 불균형 데이터 내 소수 클래스(부적합) 탐지에 훨씬 효과적임을 입증함.*
