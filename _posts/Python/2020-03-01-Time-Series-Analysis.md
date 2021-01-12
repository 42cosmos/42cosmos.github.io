---
layout: post
title: 'Time Series with python'
tags: [TimeSeries]
categories: 'Python'
---

### 시계열 데이터 분석

독립변수 / 종속변수  +  **시계열 데이터**   



1. 정상 시계열
   - 뚜렷한 추세 없음
   - 시간 흐름에 따른 동일한 진폭
2. 비정상 시계열
   - 시간에 따른 데이터의 변화
   - 추세와 시간대 존재
   - 평균 수준이 시간대에 따라 다르다
   - 가변적 분산

**비정상 시계열일 경우 반드시 정상 시계열로의 변환 필요**



#### 비정상 시계열의 정상화

1. 분산이 일정하지 않은 경우

   : 분산안정화변환 ( 로그, 제곱근, Box-cox 변환 시도)

2. 추세를 가지는 경우
   - 결정적 추세 > 분해법 또는 추세항 모형에 포함
   - 확률적 추세 ( Dickey-Fuller의 단위근 검정 ) > 차분
3. 계절성을 가지는 경우
   - 결정적 계절 추세 > 계절 추세항 모형에 포함
   - 확률적 계절 추세 ( 계절형 단위근 검정 ) > 계절차분



#### ARIMA 

- **A**uto **R**egression **I**ntergrated with **M**oving **A**verage

> ARIMA(p, d, q) > 모수 설정



#### in Pandas

1. arima 모형은 반드시 series 형태를 전제함
2. 데이터 타입을 float으로 변경

