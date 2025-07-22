
# 🚲 자전거 대여량 예측 모델 (시간대 기반)

## 📌 프로젝트 개요

이 프로젝트는 `Kaggle Bike Sharing Demand` 데이터를 바탕으로, 날짜 및 기상 정보를 활용하여 **시간 단위 자전거 대여 수요(count)를 예측**하는 머신러닝 회귀 모델을 구축하였습니다.

---

## 📂 데이터 개요

- **train.csv** : 2011-01-01 ~ 2012-12-19까지의 학습용 데이터 (datetime, weather, temp, count 등 포함)
- **test.csv** : 2012-12-20 ~ 2012-12-31까지의 테스트 데이터
- **sub.csv** : 예측 결과 제출용 파일 (`datetime`, `count` 컬럼 포함)

---

## 🔍 주요 전처리 과정

### ✅ 범주형 처리
- `season`, `holiday`, `workingday`, `weather`는 `category`로 변환
- 계절이나 휴일은 연속성을 가지고 잊지 않기 때문에 회귀 모델이 오해하지 않도록 범주형으로 처리

### 🕒 시간 파생 변수 생성
- `datetime` → `hour`, `day`, `dayofweek`, `sunday` 생성
- `daypart`: 시간대를 아침/오전/저녁/야간(4분할)로 구분
-  datetime 변수에서 여러 파생변수를 생성하였으며 시간은 4분할로 구분하였습니다 

### 📊 최종 Feature 구성
```python
[
    'season', 'holiday', 'workingday', 'weather',
    'temp', 'atemp', 'humidity', 'windspeed',
    'time', 'day', 'sunday', 'hour', 'daypart'
]
```

---

## 🧠 모델링

### 🎯 사용 모델
- `RandomForestRegressor`
- `LinearRegression`

### 🧪 교차 검증 및 평가
- `mean_squared_log_error (RMSLE)` 활용
- 모델 비교 실험 및 예측 결과 도출

---

## 📈 주요 결과

예측 결과(`sub.csv`)는 테스트셋의 `datetime`에 대응하는 대여량(`count`)을 포함합니다. 모델 성능 향상을 위해 다양한 특성 조합과 모델 실험이 포함되어 있으며, 주로 RandomForest 기반 예측이 높은 성능을 보였습니다.

---

## 📁 프로젝트 구조

```
├── 시간별 자전거 대여예측 모델_복습.ipynb  # 주요 분석 및 모델링 노트북
├── sub.csv                                   # 예측 결과 제출 파일
└── README.md                                 # 프로젝트 설명 파일
```

---

## 🚀 향후 개선 방향

- LightGBM, XGBoost 등 Gradient Boosting 모델 도입
- 시간대별 계절성과 날씨 상호작용 추가
- 로그 변환 등 비선형 특성에 대한 고려

---

## 📝 참고

- 데이터 출처: [Kaggle - Bike Sharing Demand](https://www.kaggle.com/c/bike-sharing-demand)
- 분석 도구: Python, scikit-learn, pandas, matplotlib 등

