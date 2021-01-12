---
layout: post
title: 'Selenium [5] Practice'
categories: 'Web_Scraping'
image: 
tags: [selenium, web scraping]
---

### 네이버 기사 댓글 크롤링

`options.add_argument('headless')`

헤드리스 옵션을 넣을 때와 그렇지 않을 때 가져오는 데이터의 차이가 나타났다. 왜? 저 한 줄을 고작 주석처리 할 뿐이었는데 어떻게 고쳐야하는지 모르겠다. 

headless 일 때 가져오는 댓글의 수 겨우 10개. 없을 때는 내가 원하는 만큼 잘 가져온다. ... 음... 도대체 왜?