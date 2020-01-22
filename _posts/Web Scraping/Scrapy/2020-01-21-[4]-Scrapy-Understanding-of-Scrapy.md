---
layout: post
title: '[4] Scrapy Practices '
categories: [Study/Web Scraping]
tags: [scrapy, web scraping]

---

### others

1. 필드명 순서의 랜덤 : DB 안에 넣는 데이터라 크게 신경쓰지 않아도 됨. 그럼에도 불구하고 원하는 순서가 있다면 `settings.py` 안에 `FEED_EXPORT_FIELDS = ['a', 'b', 'c'] ` 선언
2. 동시 크롤링 횟수 조정 
    `settings.py` 안에 `#CONCURRENT_REQUESTS = n`  주석 해제 후 숫자 변경 > 단, 속도 저하 

 