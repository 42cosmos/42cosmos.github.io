---
layout: post
title: 'BeautifulSoup 네이버 블로그 검색결과 가져오기'
tags: [BeautifulSoup, python]
categories: [Study/Web Scraping]
---

### BeautifulSoup

---

가장 기본 형식 - 검색어 고정 형태

```python
import urllib.request
from bs4 import BeautifulSoup

url = 'https://search.naver.com/search.naver?where=post&sm=tab_jum&query=python'
html = urllib.request.urlopen(url).read() # Html 가져오기
soup = BeautifulSoup(html, 'html.parser')

title = soup.find_all(class_='sh_blog_title')

for i in title:
    print(i.attrs['title'])
    print(i.attrs['href'], end='\n\n')

```



#### 검색어 변경 (part)

```python
base_url = 'https://search.naver.com/search.naver?where=post&sm=tab_jum&query='
plus_url = input('검색어 입력')
url = base_url + urllib.parse.quote_plus(plus_url)	
```

**urllib.parse.quote_plus()** 



#### 네이버 이미지 저장하기

```python
base_url = 'https://search.naver.com/search.naver?where=image&sm=tab_jum&query='
plus_url = input('search')
url = base_url + quote_plus(plus_url)

html = urlopen(url).read()
soup = BeautifulSoup(html, 'html.parser')

img = soup.find_all(class_ = '_img')

count = 1
for i in img:
    img_src = i['data-source']
    with urlopen(img_src) as file:
        with open('./photo/' + plus_url + str(count) + '.jpg', 'wb') as img_file: # 이미지기 때문에 binary
            file_read_img =file.read()
            img_file.write(file_read_img)
    count += 1
# 개발자 도구에서 보는 것과 실제 소스분석과 다를 수 있음.
# 출력을 하면서 봐야 함.
```



