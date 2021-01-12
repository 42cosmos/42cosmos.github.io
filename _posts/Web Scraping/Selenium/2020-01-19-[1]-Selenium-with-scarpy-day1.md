---
layout: post
title: 'Selenium [1] 크롤링 기본'
categories: 'Web_Scraping'
tags: [selenium, web scraping]
---

#### 웹페이지 가져오기

- `requests.get('url')`

<br>

#### 웹페이지 파싱하기

- 파싱 == 문자열 의미 분석
- bs 라이브러리 사용
  - `'BeautifulSoup('var', 'html.parser)'`

<br>

#### 데이터 추출

- `soup.find()` 함수로 원하는 부분 지정
- `.get_text()` 함수로 추출 부분 가져옴



**필요 데이터 추출 방법**

1. 태그와 속성으로 선택

- `.find('tag')`
- `.find(id='tag')`
- `.find('p', class='css.tag')`
- `.find('p', attrs = {'align' : 'center'})`

2. CSS Selector로 선택

+ `.select('html > title')`
+ `.select('div.article_view')`
+ `.select('#harmonyContainer')`
+ `.select('div#mArticle')`



#### 브라우저

+ javascript 코드 이해 동반
+ 브라우저를 통한 요청 > 난이도 하향 가능



