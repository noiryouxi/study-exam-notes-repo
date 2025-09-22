# 분석모형 평가 및 개선

## 1. 분석모형 평가

### 1.1 분류모델 평가지표

- **혼동행렬 (Confusion Matrix)**
  - TP (True Positive), FP (False Positive), FN (False Negative), TN (True Negative) 기반 지표
  - **재현율(Recall)** = TP / (TP + FN)  
    : 실제 Positive 중 맞춘 비율 (민감도, Sensitivity, TP Rate)
  - **정밀도(Precision)** = TP / (TP + FP)  
    : Positive로 예측한 것 중 실제 Positive 비율
  - **F1 Score** = 2 × (Precision × Recall) / (Precision + Recall)  
    : 정밀도와 재현율의 조화평균 (불균형 데이터에 유리)
  - **특이도(Specificity)** = TN / (TN + FP)  
    : 실제 Negative 중 맞춘 비율
  - 정밀도와 재현율은 Trade-off 관계

- **ROC Curve (Receiver Operating Characteristic Curve)**
  - 가로축: 1 - Specificity (= FPR), 세로축: Recall (= TPR)
  - **AUC (Area Under Curve)**: 1에 가까울수록 모델 성능 우수

- **이익 도표 (Lift Table)**
  - 불균형 데이터셋에서 사용
  - 각 등급별 예측 성능 향상 정도 확인
  - **Lift Curve**: 이익 도표 시각화

---

### 1.2 회귀모델 평가지표

- **손실함수 / 비용함수 (Loss / Cost Function)**
  - MAE (Mean Absolute Error)
  - MSE (Mean Squared Error)
  - RMSE (Root Mean Squared Error)

- **결정계수 (R², R-Square)**
  - 설명력 지표 (0~1 범위, 1에 가까울수록 설명력 높음)

---

### 1.3 군집분석 평가지표

- **군집 내 유사성**, **군집 간 분리성** 평가

- **실루엣 계수 (Silhouette Coefficient)**
  - -1~1 사이 값, 0.5 이상이면 타당한 군집화

- **Dunn Index**
  - 군집 간 거리 / 군집 내 거리  
  - 클수록 우수한 군집화

---

### 1.4 교차 검증 (Cross-Validation)

| 방식 | 설명 |
|------|------|
| 홀드아웃 | 데이터를 훈련용과 테스트용으로 분리 |
| K-Fold | 전체 데이터를 K개로 나누어 교차 학습/평가 |
| LOOCV (Leave-One-Out) | 1개의 데이터만 테스트, 나머지는 학습 |
| 부트스트랩 | 복원추출 기반 샘플링 (데이터 부족/불균형 해결에 도움) |

---

### 1.5 적합도 검정 (Goodness of Fit)

- **Q-Q Plot**: 정규성 여부 시각적으로 판단 (대각선 근처 분포 → 정규성 만족)
- **Shapiro-Wilk 검정**
  - p-value > 0.05 → 정규성 만족
- **Kolmogorov-Smirnov 검정**
  - 누적 분포함수 비교
  - p-value > 0.05 → 정규성 만족
- **Chi-square (카이제곱) 검정**: 범주형 데이터의 기대빈도와 관측빈도 비교

---

## 2. 분석모형 개선

### 2.1 하이퍼파라미터 조정

- **학습률 (Learning Rate, α)**  
  - 너무 크면 발산, 너무 작으면 학습 느림
- **Batch Size**
  - 한 번의 학습에 사용하는 데이터 수
- **Epoch**
  - 전체 데이터셋을 몇 번 학습할지
- **Iteration**
  - 1 Epoch에서 몇 번의 배치가 필요한지

#### 하이퍼파라미터 튜닝 방법

| 방법 | 설명 |
|------|------|
| 매뉴얼 서치 | 경험 기반 수동 설정 |
| 그리드 서치 (Grid Search) | 후보군 전체 탐색 |
| 랜덤 서치 (Random Search) | 랜덤한 조합 탐색 |
| 베이지안 최적화 | 이전 결과 바탕으로 확률적 탐색 |

---

### 2.2 경사하강법 최적화 알고리즘

- **SGD (Stochastic Gradient Descent)**: 무작위 샘플 기반 최적화
- **Momentum**: 관성 개념 적용 → 더 빠른 수렴 가능
- **AdaGrad**: 학습률 자동 조절 (기울기 클 때 학습률 작게)
- **Adam**: Momentum + AdaGrad 혼합 → 안정적이고 빠른 수렴

---

# 분석결과 해석 및 활용

## 1. 분석결과 해석

### 1.1 주성분 분석 (PCA)

- **스크리 플롯 (Scree Plot)**
  - 주성분 수 선택 시 사용
  - **팔꿈치 기법**: 기울기 변화가 완만해지기 전까지의 주성분 사용

### 1.2 회귀모형의 검정

| 검정 항목 | 지표 | 귀무가설 |
|-----------|------|-----------|
| 모형 유의성 | F-통계량, p-value | 모든 계수 = 0 |
| 회귀계수 유의성 | t-통계량, p-value | 개별 계수 = 0 |
| 설명력 | 결정계수 R² | 0~1 (높을수록 좋음) |
| 자유도 (DF) | 회귀계수 개수 및 샘플 크기 기반 산출 |  |

---

## 2. 분석결과 시각화

### 2.1 시각화 분류

| 유형 | 예시 | 목적 |
|------|------|------|
| 시간 시각화 | 막대그래프, 선그래프, 점그래프 | 시간 흐름 표현 |
| 공간 시각화 | 등치지역도, 카토그램, 버블플롯 | 지리/위치 정보 표현 |
| 관계 시각화 | 산점도, 히트맵, 히스토그램 | 변수 간 관계/분포 확인 |
| 비교 시각화 | 체르노프 페이스, 평행좌표계 | 변수 간 비교 및 유사성 분석 |

### 2.2 인포그래픽 (Infographic)

- 정보 + 시각적 요소 결합한 표현 방식
- **목적**: 일반인에게 직관적으로 설득력 있는 메시지 전달
- **주요 유형**
  - **타임라인**: 시간순 나열
  - **컨셉 맵**: 주제 간 연관성 중심 표현

---