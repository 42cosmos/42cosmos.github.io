---
layout: post
title: 'Scrapy [2] web crawling issues and Scrapy structure '
categories: 'Web_Scraping'
tags: [scrapy, web scraping]
---

### 웹 크롤링 이슈

**저작권법 허용**

1. 단순 링크 
2. 직접 링크 : 특정 게시물 링크

**저작권법 위반**

1. 프레임 링크 - 저작물 일부를 홈페이지 표시
2. 임베드 링크 - 저작물 전체를 홈페이지 표시



크롤링 데이터 임의적 사용은 괜찮지만, 어딘가에 게시할 때는 주의하여야 함. 



### 로봇 배제 표준 (robots.txt)

크롤링 허용 확인 - 게시물에 대한 권한이 누구에게 있는가? 

유저와 운영자의 이해관계 차이 존재 

<br>

1. 모두 허용  
   User-agent:  
   Allow:

   

2. 모두 차단  
   User-agent:  
   Disallow:  

   

3. 조합    
   User-agent: googlebot    # googlebot 로봇만 적용
   Disallow: /private/     # 이 디렉토리를 접근 차단한다.
   User-agent: googlebot-news  # googlebot-news 로봇만 적용
   Disallow: /         # 모든 디렉토리를 접근 차단한다.
   User-agent: *        # 모든 로봇 적용
   Disallow: /something/    # 이 디렉토리를 접근 차단한다.출처 : [위키/로봇 배제 표준](https://ko.wikipedia.org/wiki/로봇_배제_표준)



### Scrapy 구조

/spiders - 실제 크롤링 로직이 들어감

items.py - 크롤링 대상 저장

pipelines.py - 크롤링 결과를 DB 삽입 혹은 필터링 결정

settings.py - 전체 프로젝트 설정 : 파이프라인 순서 결정, 로그 파일 지정 및 레벨 변경 등 

scrapy.cfg - 전체 프로젝트 배포 시 설정



#### 동작

1. items.py 정의 
2. /spiders 안에 시작 url 지정 (start_requests - 특정 url에 대한 callback함수 지정 가능, start_urls - 스트링 리스트, ), 각 url에 대한 callback 함수 지정 (parse() - common)
3. callback 함수 정의  
   selector를 이용해 데이터 선택 (xpath, css)
4. Pipeline을 통해 데이터 필터링 혹은 DB에 저장



#### Spiders

- 크롤러 이름 지정 
  - name
- 스타트 url 지정
  - start_requests :
    - 콜백 함수 지정 가능
    - 사이트 로그인 시 사용
  - start_urls :
    - 시작 주소를 리스트 형태로 추가
- parser 정의
  - def parser(self, response):



#### Selector

html 문서에 특정 노드 선택

**css vs xpath**

```
>>> response.xpath('//title/text()')
>>> response.css('title::text')

>>> response.xpath('//base/@href').extract()
>>> response.css('base::attr(href)')

>>> response.xpath('//a[contains(@href, "image")]/@href')
>>> response.css('a[href*=image]::attr(href)').extract()

>>> response.xpath('//a[contains(@href. "image")]/img/@src').extract()
>>> response.scc('a[href*=image] img::attr(src)').extract()
```





#### Pipeline

데이터 크롤링 이후 특정 행동 수행

1. 데이터 유효성 검사
2. 중복 체크
3. DB 저장
4. 필터링

**settings.py**

1. 파이프 클래스 및 순서 지정	

   ITEM_PIPELINES = {

   'project_name.pipelines.CommunityPipline' : 200,

   } > 숫자가 낮을 수록 선실행

   

   

#### Logging

- settings.py

  - LOG_FILE = 'logfile.log'

  - LOG_LEVEL = logging.DEBUG

    설정파일에 파일명과 로그레벨을 통해 정의가 가능

- Log Level

  1. logging.CRITICAL - for critical errors (highest severity)
  2. logging.ERROR - for regular errors
  3. logging.WARNING - for warning messages
  4. logging.INFO - for informational messages
  5. logging.DEBUG - for debugging messages (lowest severity)

  > LOG_LEVEL = logging.WARNING 이라고 설정하면 1~3까지가 지정됨

  