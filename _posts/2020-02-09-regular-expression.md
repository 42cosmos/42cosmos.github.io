---
layout: post
title: 'Regular Expression'
---

[생활코딩 정규표현식](https://www.inflearn.com/course/생활코딩-정규표현식/dashboard)



### 문자 처리 작업 

1. 찾고자 하는 텍스트 삽입
2. case sensitive 
3. ^ 첫 번째 - 시작 위치 지정
4. $ - 마지막 위치지정

5. \ -escape reserved word

6. . - matches any character 

7. ...... - any char with 6

8. \\..\\. - .(str) any .(str)

9. [] - brackets 특정 문자 - 원하는 문자 후보군 

10. [ - ] - A range of char

    1. [C-K] : choose C to K
    2. [2-6] : choose 2 to 6
    3. [A-Za-z0-9] 

11. ^ in brackets - Specified chars will not be selected 

    1. [^C-Z] choose without C to Z
    2. [^picture] - choose without 'picture'

12. sub pattern 

    src : Monday Tuesday Friday

    1. (on|ues|rida)
    2. (Mon|Tues|Fri)day 
    3. ..(id|esd|nd)ay

13. Quantifiers \*

    1. a*b - *앞 패턴의 등장 횟수 0 - ∞
    2. a+b - 1 - ∞
    3. a?B - 0 - 1

    - .\* : 모든 텍스트
    - -A*- : - 앞에 A의 등장 횟수가  0 - ∞일 수 있음, 반드시 -는 A의 앞에 있어야 함
    - [-@]\* : 문자 중 - or @ 를 선택하고, 이 한 글자에 대한 패턴을  0 - ∞ 개 찾음
    - \\\*+ : 뒷 문자를 단순 문자로 하고, 앞 \*가  1 - ∞ 임을 선택
    - -@+- : 앞 뒤 반드시 -가 오고, @는 한 개 이상이어야 함
    - [^ ]+ : 공백이 아닌 것 한 개 이상 선택 / 공백 제외 모든 것 출력
    - -X?XX?X : - 뒤 X는 0 - 1개 오며 중간에 X가 필수로 있음, 이어 오는 X는 0 - 1개 오며, 뒤에 X가 필수로 있음