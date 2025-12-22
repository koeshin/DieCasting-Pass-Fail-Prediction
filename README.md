# 다이캐스팅 공정 데이터 분석을 통한 불량률 예측

본 프로젝트는 다이캐스팅(Die Casting) 제조 공정 데이터를 분석하여, 제품 불량률(Pass/Fail)에 영향을 미치는 주요 변수를 탐색하고 머신러닝 모델을 통해 불량을 예측하는 것을 목표로 합니다.

## 데이터셋

  * **데이터 출처:** [KAMP AI - 주조 공정 최적화 데이터셋](https://www.google.com/search?q=https://www.kamp-ai.kr/aidataDetail%3FAI_SEARCH%3D%25EC%25A3%25BC%25EC%25A1%25B0%2B%26page%3D1%26DATASET_SEQ%3D53)
  * **데이터 설명:** 주조 공정 중 다이캐스팅 방법으로 생산된 제품의 공정 변수(온도, 속도, 압력 등)와 그에 따른 품질검사 결과(Pass/Fail) 데이터입니다.

## 분석 프로세스

분석은 다음과 같은 순서로 진행되었습니다.

### 1\. 데이터 전처리 (Data Preprocessing)

  * 결측치 및 이상치를 확인하고 처리했습니다.
  * 왜도가 높은 주요 변수(`cast_pressure` 등)에 대해 로그 변환(Log Transformation)을 적용하여 데이터 분포를 정규화했습니다.

### 2\. 탐색적 데이터 분석 (EDA)

  * **Target 분포 확인:** `matplotlib`, `seaborn`을 사용하여 Pass/Fail 타겟 변수의 분포를 시각화한 결과, 데이터가 심각하게 불균형함(Imbalanced Data)을 확인했습니다.
  * **주요 변수 분석:** 피벗 테이블과 시각화를 통해 `cast_pressure`, `low_section_speed` 등의 변수가 Pass/Fail 그룹 간 유의미한 평균 차이를 보임을 확인했습니다.
  * **변수 간 관계 분석:** 주요 변수들의 분포와 관계를 시각화하여 품질에 영향을 미치는 요인을 탐색했습니다.

### 3\. 데이터 불균형 처리

  * 데이터 불균형 문제를 해결하기 위해 **SMOTE (Synthetic Minority Over-sampling TEchnique)** 기법을 적용하여 소수 클래스(Fail) 데이터를 오버샘플링했습니다.

### 4\. 머신러닝 모델링 (Modeling)

  * 데이터셋을 학습(Train) 및 테스트(Test) 세트로 분리한 후, 다음 모델들을 학습시켰습니다.
      * **Logistic Regression**
      * **Random Forest**
      * **XGBoost**

### 5\. 모델 평가 (Evaluation)

  * **성능 비교:** `Classification Report` (Precision, Recall, F1-Score)를 통해 각 모델의 성능을 평가했습니다. 불균형 데이터를 고려하여 F1-Score를 핵심 지표로 사용했습니다.
  * **변수 중요도 (Feature Importance):** Random Forest와 XGBoost 모델의 변수 중요도를 시각화하여 어떤 변수가 불량 예측에 가장 큰 영향을 미치는지 확인했습니다.

## 주요 분석 결과

  * **핵심 변수:** `cast_pressure` (주조 압력) 관련 변수들이 제품의 Pass/Fail을 예측하는 데 가장 중요한 요인임을 확인했습니다.
  * **모델 성능:** SMOTE로 불균형을 처리한 후 학습시킨 **XGBoost**와 **Random Forest** 모델이 가장 우수한 예측 성능(F1-score)을 보였습니다.
