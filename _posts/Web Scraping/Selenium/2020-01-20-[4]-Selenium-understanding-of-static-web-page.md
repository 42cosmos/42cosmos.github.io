---
layout: post
title: '[4] Selenium Understanding of static web page'
categories: [Study/Web Scraping]
image: 
tags: [selenium, web scraping]
---

### Ajax과 같은 동적 웹페이지 데이터 로딩

"웹페이지 새로고침 X > 특정 부분만 변경"

특정 부분을 동적으로 가져오고, 해당 부분만 변경 시 그 부분만 변화 == 댓글 등

웹브라우저에 전부 로딩 시킨 후 가져올 수 있음



### 동적 데이터 특징-필요조건

전체 html 파일 로딩과의 시간차 발생 > 해당 데이터를 불러올 때까지 기다리는 함수(클래스, 객체) 필요 && 줄여진 댓글창 '더보기' > 원하는 댓글 수보다 댓글이 없을 때 해야할 기능



#### 특정 태그 일정 시간 기다리기

```python
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

element = WebDriverWait(driver, 3).until(EC.presence_of_element_located((By.ID, "alex-area")) 
)
```

(By.ID, "alex-area") : ( 기다릴 객체, "객체 이름")



#### 특정 태그 존재 여부 확인 기능

```python
from selenium.webdriver.common.by import By
```

+ By.CLASS_NAME: class name
+ By.CSS_SELECTOR: css selector
+ By.ID: id
+ By.NAME: name
+ By.TAG_NAME: tag name



```python
from selenium.common.exceptions import TimeoutException

try:
	element = WebDriverWait(driver, 3).until(EC.presence_of_element_located((By.CSS_SELECTOR, "a")) )
  more_button = driver.find_element_by_css_selector("a") 
  more_button.click()
  count += 1
  
except TimeoutException:
  loop = False
```



#### 키보드-마우스 동작 자동화 (ActionChains)

`actions = webdriver.ActionChains(driver)` : 변수 선언 후 정적 데이터(버튼)를 갖고 있는 변수를 `actions.click(var_name)` 클릭 함수 내 인자값으로 삽입 > `actions.perform()` 삽입이 반드시 필요함

== `webdriver.ActionChains(driver).click(var_name).perform()`



#### 브라우저 내에서 pause

```python
from selenium.webdriver.support.ui import WebDriverWait
from selenium.common.exceptions import TimeoutException
```

TimeoutException은 WebDriverWait를 함수로 기다릴 때 일정 시간이 지났는데도 태그가 나타나지 않을 때 (예외 상황)



