---
layout: post
title: 'Scrapy [4] Practices'
categories: 'Web_Scraping'
tags: [scrapy, web scraping]

---

### others

1. 필드명 순서의 랜덤 : DB 안에 넣는 데이터라 크게 신경쓰지 않아도 됨. 그럼에도 불구하고 원하는 순서가 있다면 `settings.py` 안에 `FEED_EXPORT_FIELDS = ['a', 'b', 'c'] ` 선언
2. 동시 크롤링 횟수 조정 
    `settings.py` 안에 `#CONCURRENT_REQUESTS = n`  주석 해제 후 숫자 변경 > 단, 속도 저하 




### 데이터 후처리

정규표현식

```python
import re

def parse(self, response):
  data = json.loads(response.body_as_unicode())
  for item in data['items']:
    print(re.sub('</S+>', '', item['title']))
```



### JSON 데이터 크롤링 처리

```python
import json

def parse(self, response):
  data = json.loads(response.body_as_unicode())
  for item in data['items']:
    doc = Naveropenapiitem()
    doc['title'] = item['title']
    doc['link'] = item['link']
```

`loads()`함수로 가져오면서 `body_as_unicode()`처리

for문으로 json 데이터를 한 개씩 쪼개서 입력 가능



### Naver openapi - 요청변수

```python
for index in range(10):
  yield scrapy.Request(url=url + words_var + '&display=100&start=' + str(index*100 + 1), headers=header_var)
```

'&display=100&start=' + str(index*100 + 1)  처럼 작성 가능 >> 

1. 0 > 1부터 100개
2. 1 > 101부터 100개 
3. 2 > 201부터 100개





### 숙제

\<b>,\n, \t ... 등의 태그 없애기