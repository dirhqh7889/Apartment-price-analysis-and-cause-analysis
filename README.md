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
1. 2013.9~2015.8까지 전국 평균 분양가격, 2015.10-2020.4까지 전국 아파트 분양가격을 합친 데이터는 [지역명-연도-월-평당분양가격] 모델링
2. 2013~2020.10까지 아파트 전세가격지수는 [지역-연도-월-지역별전세가격] 모델링
3. 2015~2020.9까지 미분양주택현황통계는 [지역명-연도-월-미분양주택갯수] 모델링
4. 3가지 데이터를 비교하기 위해 [지역명-연도-월]을 일치하게 모델링하였고 수치값을 비교하기 위해 각각 [평당분양가격, 지역별전세가격, 미분양주택갯수]로 모델링하였다.

## 시각화 및 탐색
### 전국 그래프

**1. 전국 분양가격 그래프**   
![분양가격 그래프](https://user-images.githubusercontent.com/59160781/100536810-6a83af00-3266-11eb-82d8-987ec56f6a5c.PNG)   
  * 위 그래프는 전국의 분양가격을 보여주는 그래프이다. 서울을 비롯해 모든 시,도가 상승 곡선을 타고 있는 것을 볼 수 있다. 
    그중 유독 서울이 다른 시,도에 비해 가격이 많이 높다는 것을 확인할 수 있다.   
        
**2. 전국 전세가격 그래프**   
![전세가격 그래프](https://user-images.githubusercontent.com/59160781/100536825-8ab36e00-3266-11eb-8eba-e70d0772f4a2.PNG)   
  * 위 그래프에서 전국의 전세가격 그래프이다. 2013년부터 모두 상승곡선을 타다가 2016,17년도부터 주춤하는 것을 볼 수 있다.
    그런데 다시 2019년부터 상승곡선이 시작된 것을 볼 수 있다.   
        
**3. 전국 미분양주택 그래프**   
![전국 미분양주택 그래프](https://user-images.githubusercontent.com/59160781/100537433-09f77080-326c-11eb-94d9-2011cf584817.PNG)   
  * 위 그래프는 전국의 미분양주택갯수 그래프이다. 지역마다 표준편차가 너무 커서 모두 표시가 되지 않았다.   
      
### 서울 그래프
**1. 서울 분양가격 그래프**   
![서울 분양가격 그래프](https://user-images.githubusercontent.com/59160781/100536984-d4508880-3267-11eb-809a-0c18a28574fe.PNG)    
  * 위 그래프는 서울의 분양가격 그래프이다. 2013년부터 꾸준히 상승곡선을 타고 있는 것을 볼 수 있다.
    천천히 상승하다가 2018-2019년에 급작스럽게 상승을 했고 2020은 미약하게 상승을 했다.   
        
**2. 서울 전세가격 그래프**   
![서울 전세가격 그래프](https://user-images.githubusercontent.com/59160781/100536930-55f3e680-3267-11eb-8492-3262646c3390.PNG)   
  * 위 그래프는 서울의 전세가격 그래프이다. 상승곡선을 꾸준히 타다가 2018-2019년에 잠시 내려간 것을 볼 수 있고
    2020년에는 다시 상승한것을 볼 수 있다.   
        
**3. 서울 미분양주택 그래프**   
![서울 미분양주택 그래프](https://user-images.githubusercontent.com/59160781/100537276-5e015580-326a-11eb-8bc8-a46b7355a83a.PNG)   
  * 위 그래프는 서울의 미분양주택 그래프이다. 이 그래프는 하락곡선을 보여주고 있다. 2015년부터 2018년까지 꾸준히 내려다가다 
    2019년에 잠시 올라갔고 다시 2020년에 떨어진 것을 볼 수 있다.   
        













