---
layout: post
title: '머신러닝을 위한 Python 03'
tags: [ML, Python]
categories: [Study/Python]
---

*Scala*는 이탤릭체, **vector**는 소문자 볼드, **MATRIX**는 대문자 볼드



기존 데이터를 알고리즘을 사용해 모델을 만들고, 새 데이터에 모델을 적용해 예측하는 것 : 핵심은 알고리즘과 모델

y = ax + b 꼴의 선 ? x = '보고싶어요' y = 총 관객 수 > a, b를 알아내는 것



### Key concepts

모델 : 예측을 위한 수학 공식, 함수, condition rule처럼 조건일 수도 있음

알고리즘 : 모델을 만들기 위한 과정



Y에 영향을 주는 X의 값은 하나인가?



### Feature - 독립변수

데이터 특징을 나타내는 변수 : input 변수

데이터 테이블 상에서 컬럼을 의미

엑스와 와이를 갖고 있는 상황에서 베타를 알게하는 것



### Feature Vector

전체 데이터 셋에서 0번째를 표현한 수식

선형대수의 표기법을 사용 >

list=w^t x=list >로 표현해 y의 예측치를 찾아낼 수 있을 것임
