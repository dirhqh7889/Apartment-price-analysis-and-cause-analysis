# Apartment-price-analysis-and-cause-analysis
# 아파트 분양가격 2013~2020 비교 및 원인분석

## 문제정의
현재 아파트 가격 상승이 많은 이슈가 되고 있다. 코로나로 인해 경제도 좋지 않은 상황에 어째서 아파트 가격이 상승하는지 원인을 분석해볼 것이다.

## 데이터 수집
데이터는 공공데이터 포털을 통해 얻었다.   
공공데이터 포털은 공공데이터를 한 곳에서 제공하는 통합 창구로 쉽고 편리하게 공공데이터를 얻을 수 있다.   
수집한 데이터:   
1. 2013.9-2015.8까지 전국 평균 분양가격
2. 2015.10-2020.4까지 전국 아파트 분양가격
3. 2013-2020.10까지 아파트 전세가격지수
4. 2015-2020.9까지 미분양주택현황통계를 이용하였다.
공공데이터 포털: https://www.data.go.kr/

## 데이터 전처리
수집한 데이터를 전처리하여 결측치와 이상치를 처리하였고 데이터를 연계하였다.
1. 2013.9-2015.8까지 전국 평균 분양가격, 2015.10-2020.4까지 전국 아파트 분양가격을 합쳐 하나의 데이터로 만들었다.
2. 2013.9-2015.8까지 전국 평균 분양가격, 2015.10-2020.4까지 전국 아파트 분양가격을 합친 데이터에서 분양가격(㎡)열이 object데이터로 되어 있어 수치 데이터로 바꾸는 과정에서 결측치(공백) 값이 있어 에러가 발생하였고 에러를 무시하도록 만듬으로써 안전하게 수치값으로 바꾸었다. ex) pd.to_numeric(df_last["분양가격(㎡)"], errors = 'coerce')
3. 2013-2020.10까지 아파트 전세가격지수에서 하나의 열 전체가 결측치인 부분이 있어 열 전체를 삭제하였다.

## 데이터 모델링
전처리한 데이터를 모델링하였다. 
1. 2013.9~2015.8까지 전국 평균 분양가격, 2015.10-2020.4까지 전국 아파트 분양가격을 합친 데이터는 지역명-연도-월-평당분양가격으로 모델링
2. 2013~2020.10까지 아파트 전세가격지수는 지역-연도-월-지역별전세가격으로 모델링
3. 2015~2020.9까지 미분양주택현황통계는 지역명-연도-월-미분양주택갯수로 모델링
4. 3가지 데이터를 비교하기 위해 지역명-연도-월을 일치하게 모델링하였고 수치값을 비교하기 위해 각각 평당분양가격, 지역별전세가격, 미분양주택갯수로 모델링하였다.

## 시각화 및 탐색














