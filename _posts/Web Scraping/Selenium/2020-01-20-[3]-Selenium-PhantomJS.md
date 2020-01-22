---
layout: post
title: '[3] Selenium PhantomJS & Headless Chrome'
categories: [Study/Web Scraping]
image: 
tags: [selenium, web scraping]
---

### Phantom JS

화

면 없이 실행하는 프로그램 - Web testing > 시간이 단축되지는 않기에 경우에 따라 선택적 사용이 필요

- 터미널 환경에서 동작하는 크롤러에게 권장
- 최신 셀레니움은 지원을 하지 않는 상태

\* 기존 부분 `webdriver.Chrome('*')` 만 변경

*아예 안 됨!*



### Headless Chrome 

```python
options.add_argument('headless')
```

: PhantomJS와 유사한 기술로 크롬브라우저 기능으로 개발됨

\* 상동



```python
c_options = webdriver.ChromeOptions()
c_options.add_argument('headless')
driver = webdriver.Chrome(url, options=c_options)
```



`coptions.add_argument('window-size=1920x1080')` : 웹 브라우저 사이즈 지정

`coptions.add_argument('disable-gpu')` : 그래픽카드 사용 안 함

`coptions.add_argument('User-Agent: ~~')` : 서버 요청 시 헤더 재 구성

`coptions.add_argument('lang=koKR')` : 사용자 언어 