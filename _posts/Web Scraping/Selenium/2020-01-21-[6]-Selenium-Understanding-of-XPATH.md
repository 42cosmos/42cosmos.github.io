---
layout: post
title: 'Selenium [6] XPATH 이해하기'
categories: 'Web_Scraping'
image: 
tags: [selenium, web scraping]
---

### XML 특정 요소나 속성에 접근키 위한 경로 지정 언어

1. 태그 및 속성 선택

   ```
   crawling_data = soup.find('h1')
   crawling_data = soup.find(id='title')
   crawling_data = soup.find('p', class_='cssstyle') crawling_data = soup.find('p', attrs = {'align': 'center'})
   ```

   

2. CSS Selector

   ```
   crawling_data = soup.select('html > title')
   crawling_data = soup.select('div.article_view')
   crawling_data = soup.select('#harmonyContainer')
   crawling_data = soup.select('div#mArticle div#harmonyContainer')
   ```



3. XPath

   - bs 미지원 / Selenium or PhantomJS 지원

   - [xpath 문법](https://wkdtjsgur100.github.io/selenium-xpath/)

   ```
   # 문서 내 태그 검색
   title = driver.find_element_by_xpath("//title")
   
   # 절대 경로
   title = driver.find_element_by_xpath("/html/head/title")
   
   # html 태그 내 검색
   title = driver.find_element_by_xpath("/html//title")
   
   # soup.find('h3', attrs = {'class' : 'tit_s'})
   title_content = driver.find_element_by_xpath("//h3[@class='tit_view']")
   ```

