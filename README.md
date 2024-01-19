# 부동산 시장과 공유 경제의 상호작용에 대한 이해
## 1. 진행 기간
2023.10.31 ~ 2024.01.19

## 2. 사용 데이터
1. New York Airbnb Data
2. The Price Of A New York House
 
## 3. 사용 언어
Python

## 4. 분석 목적
부동산 시장과 공유 경제의 상호작용에 대한 이해를 통해 지역별 부동산 투자 결정에 대한 통찰력 제공한다.

Airbnb의 존재가 지역 부동산 시장에 미치는 영향을 연구하여 정보와 수요에 따른 가격 변동을 이해하고, 특정 지역에서의 관광업계와 부동산 시장의 형태 비교 분석한다

## 5. 데이터 설명
### 1. New York Airbnb Data
|변수명|타입|변수 설명|
|------|---|---|
|id|int64|임대 공간 id 변수|
|host_response_time|object|host의 답장 속도|
|host_response_rate|float64|host의 답장 비율|
|host_is_superhost|object|superhost 여부|
|neighbourhood_group_cleansed|object|임대 공간 지역|
|latitude|float64|임대 공간 위도|
|longitude|float64|임대 공간 경도|
|room_type|object|방 종류|
|accommodates|int64|수용 인원|
|bathrooms_text|object|화장실 종류|
|bedrooms|float64|침실 수|
|beds|float64|침대 수|
|amenities|int64|편의시설 수|
|price|float64|임대 공간 가격|
|availability_90|int64|연중 이용 가능 일수(최대 90일)|
|availability_365|int64|연중 이용 가능 일수(최대 365일)|
|number_of_reviews|int64|후기 개수|
|review_scores_rating|float64|전체 평점|
|review_scores_accuracy|float64|정확도|
|review_scores_cleanliness|float64|청결도|
|review_scores_checkin|float64|체크인|
|review_scores_communication|float64|의사소통|
|review_scores_location|float64|위치|
|review_scores_value|float64|가격 대비 만족도|
|instant_bookable|object|즉시 예약 가능 여부|
|price_B|object|임대 공간 가격 이진값|

### 2. The Price Of A New York House
|변수명|타입|변수 설명|
|------|---|---|
|BOROUGH|object|부동산 위치|
|BUILDING_CLASS_CATEGORY|object|부동산 종류|
|BUILDING_CLASS_AT_PRESENT|object|건물 분류|
|TOTAL_UNITS|int64|총 단위 수|
|LAND_SQUARE_FEET|int64|토지 면적|
|GROSS_SQUARE_FEET|int64|건물 층의 총 면적|
|YEAR_BUILT|int64|건물이 지어진 연도|
|TAX_CLASS_AT_TIME_OF_SALE|object|판매시점의 세무급|
|SALE PRICE|int64|판매 가격|
|PRICE_B|object|판매 가격 이진값|

## 6. Airbnb 숙소 가격 분석 결론
### 랜덤 포레스트 모델
![랜덤포레스트](https://github.com/ParkJongHyeok99/Data_Analysis_Airbnb/assets/95224718/a9f4065b-2016-448c-95d6-1c6d28314fad)
숙소 가격에 영향을 미치는 요인
1. 방의 종류
2. 수용인원
3. 편의시설 수
4. 침실 수
5. 침대 수

### 머신러닝 모델 정확도 및 최적 파라미터
|모델명|정확도|최적 파라미터|
|------|---|---|
|결정 트리|0.81454|{'criterion': 'entropy', 'max_depth': 9}|
|로지스틱 회귀|0.80275|{'penalty': 'none', 'solver': 'lbfgs'}|
|로지스틱 회귀 (표준화)|0.81308|{'penalty': 'none', 'solver': 'lbfgs'}|
|신경망 (표준화)|0.83613|{'activation': 'logistic', 'alpha': 0.01, 'solver': 'adam'}|
|K-최근접 이웃 (표준화)|0.83019|{'n_neighbors':17}|

### 이진 분류 머신러닝 모델 정확도 및 최적 파라미터
|모델명|정확도|ROC AUC|최적 파라미터|
|------|---|---|------|
|랜덤 포레스트|0.85006|0.92615|{'max_depth': 24, 'n_estimators': 200}|
|그레디언트 부스팅|0.84723|0.92579|{'learning_rate': 0.1, 'max_depth': 12, 'n_estimators': 200}|
|라쏘 (로지스틱 회귀)|0.80817|0.88493|{'C': 1, 'solver': 'liblinear'}|
|신경망 (tf.keras)|0.83622|0.91674||
|서포트 벡터 머신|0.83690|0.91320|{'C': 10, 'gamma': 'auto', 'kernel': 'rbf'}|

## 7. New York 주택 가격 분석 결론
### 그레디언트 부스팅
![부동산_그레디언트_부스팅](https://github.com/ParkJongHyeok99/Data_Analysis_Airbnb/assets/95224718/0da8d0e3-8905-400b-a701-aeab3f242d4f)

주택 가격에 영향을 미치는 요인
1. 건물 층의 총 면적
2. 지어진 연도
3. 토지 면적
4. 지역
5. 빌딩 종류

### 머신러닝 모델 정확도 및 최적 파라미터
|모델명|정확도|최적 파라미터|
|------|---|---|
|결정 트리|0.67168|{'criterion': 'entropy', 'max_depth': 8}|
|로지스틱 회귀|0.62818|{'penalty': 'none', 'solver': 'lbfgs'}|
|로지스틱 회귀 (표준화)|0.63883|{'penalty': 'none', 'solver': 'saga'}|
|신경망 (표준화)|0.67365|{'activation': 'relu', 'alpha': 0.0001, 'solver': 'adam'}|
|K-최근접 이웃 (표준화)|0.67633|{'n_neighbors':28}|

### 이진 분류 머신러닝 모델 정확도 및 최적 파라미터
|모델명|정확도|ROC AUC|최적 파라미터|
|------|---|---|------|
|랜덤 포레스트|0.68188|0.76077|{'max_depth': 17, 'n_estimators': 200}|
|그레디언트 부스팅|0.68090|0.75943|{'learning_rate': 0.01, 'max_depth': 11, 'n_estimators': 200}|
|라쏘 (로지스틱 회귀)|0.57223|0.59019|{'C': 0.1, 'solver': 'saga'}|
|신경망 (tf.keras)|0.67982|0.75338||
|서포트 벡터 머신|0.63704|0.68885|{'C': 10, 'gamma': 'auto', 'kernel': 'sigmoid'}|

## 8. 최종 결론
 1. 수요와 공급의 변화
Airbnb와 같은 공유 경제 플랫폼은 부동산 시장의 수요와 공급을 변화시킨다. 여행자들이 호텔 대신 Airbnb를 선호하면서 특정 지역에서는 숙박 시설의 수요가 늘어난다. 이로 인해 부동산 수요가 증가하고 주택 가격이 상승할 수 있다.
 2. 관광 및 지역 발전
Airbnb와 같은 공유 경제 서비스는 지역 발전을 촉진할 수 있다. 관광 명소의 경우 호스트가 숙소 대여로 인한 추가 수입을 얻을 수 있어 지역 경제에 긍정적인 영향을 미칠 수 있다. 이는 지역의 부동산 가치를 올릴 수도 있다.
 3. 규제와 법적 요인
지역 정부의 규제와 법적 요인은 공유 경제와 부동산 시장의 상호작용에 큰 영향을 미칠 수 있다. 공유 경제 플랫폼에 대한 규제를 강화하면 부동산 가격에 영향을 미칠 수 있다.
 4. 부동산 투자 및 수익
부동산 투자자들은 공유 경제 플랫폼을 통해 부동산을 투자하고 추가 수익을 얻을 수 있다. 이로 인해 부동산의 가치가 상승할 수 있다.
 5. 고용 및 경제 성장
Airbnb 호스트 등 부동산과 직접적으로 연관된 서비스를 제공하는 사람들은 지역 경제에 기여하고 새로운 일자리가 생성되어 부동산 가격에 영향을 미칠 수 있다.
