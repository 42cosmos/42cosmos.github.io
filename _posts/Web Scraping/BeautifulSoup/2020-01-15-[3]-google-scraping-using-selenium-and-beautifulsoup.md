---
layout: post
title: 'BeautifulSoup [3] 기본 구글 크롤링 w/ Selenium'
tags: [BeautifulSoup, python]
categories: 'Web_Scraping'
---

### Google Scraping using Selenium and BeautifulSoup

```python
from urllib.parse import quote_plus
from bs4 import BeautifulSoup
from selenium import webdriver

base_url = 'https://www.google.com/search?q='
plus_url = input()
url = base_url + quote_plus(plus_url)


driver = webdriver.Chrome()
driver.get(url)

html = driver.page_source
soup = BeautifulSoup(html, 'html.parser')

r = soup.select('.r')

for i in r:
    print(i.select_one('.LC20lb').text)
    print(i.a.attrs['href'], end='\n\n') # a 태그 안에 있는 href 가져오기

```

bs로만 구글 크롤링은 헤더가 있어야 함

또한 가져온 결과에서는 클래스 이름이 없음 > 결과는 있지만 클래스 이름이 달라지기 때문에 혼합 사용 권장