---
layout: post
title: 'Scrapy [1] 활용'
categories: 'Web_Scraping'
tags: [scrapy, web scraping]
---

### 웹 크롤러 Scrapy

- 파이프라인 지원 : 데이터 후처리 (필터링 등) 가능
- 로깅 정보 확인 가능
- 상대적으로 bs보다 간편함
- 안정적 크롤링 가능 
- 시간 단축 > 동시다발적 크롤링으로 인한 순서 변경 
- 다양한 포맷으로 저장 가능

Framework 

- 함수와 코드 선작성
- 특성 함수의 위치, 사용, 작성을 지정
- 

#### Beautiful Soup

- parser의 역할이 강함
- 자동으로 유니코드로 변환해서 UTF-8 출력



### 

#### Spider 

1. 이름 : 여러 가지 크롤러(spider)를 둘 수 있으므로, 각 이름을 지정
2. 페이지 주소 : 크롤링 할 주소 지정

```
scrapy genspider 'crawler_name' 'url'

# Expected Result
Created spider 'gmarket' using template 'basic' in module:
  ecommerce.spiders.gmarket
```



![scrapy_tutorial_list](/images/scrapy_tutorial_list.png)

1. items.py - 데이터를 들고올 때 클래스 형태로 만들 수 있음 
2. pipelines.py - 데이터 수집 후 후처리 필터링 입력 진행
3. settings.py - 스크래피, 스파이더 설정 : 파이프라인 순서, 이름 등의 설정
4. spider/ - 스크랩 할 내용을 프로그래밍



#### items.py

```python
import scrapy

class TutorialItem(scrapy.Item): # 상속 필수
    title = scrapy.Field()
    link = scrapy.Field()
    desc = scrapy.Field()
```

가져오려는 아이템 정의



#### /spider/new_file.py

```python
import scrapy

class linkScrap(scrapy.Spider):
    name = "dmoz" # 스파이더 이름 지정
    domain = ["dmoztools.net"]
    start_urls = [
    'https://dmoztools.net/Computers/Programming/Languages/Python/Books/',
    'https://dmoztools.net/Computers/Programming/Languages/Python/Resources/'
    ] # 스크랩 할 url 지정

    def parse(self, response):
        for i in response.xpath('//div'):
            title = i.xpath('div[3]/a/div/text()').extract()
            link = i.xpath('div[3]/a/@href').extract()
            desc = i.xpath('/div[3]/div/text()').extract()
            print("*" * 10)
            print(title, link, desc)
```



`i.xpath('/div[3]/div/text()').extract() ` 의 값은 

```
['\r\n\t\t\t\r\n                                    The primary goal of this book is to promote object-oriented design using Python and to illustrate the use of the emerging object-oriented design patterns.\r\nA secondary goal of the book is to present mathematical tools just in time. Analysis techniques and proofs are presented as needed and in the proper context.\r\n                                    ',
 '\r\n                                  ',
 '\r\n                                  ',
 '\r\n                                ',
 '\r\n                                  ',
 '\r\n                                  ',
 '\r\n                                ',
 'Health']
```

로 나오니 리스트 0번째 값 추출 후 strip()으로 내용만 추출... 하고싶었는데 빈칸이 출력됨



#### in Terminal - shell

```python
>>> scrapy shell 'url'

In [4]: response.xpath('//title').extract()                                     
Out[4]: ['<title>DMOZ - Computers: Programming: Languages: Python: Books</title>']

In [5]: response.xpath('//title')                                               
Out[5]: [<Selector xpath='//title' data='<title>DMOZ - Computers: Programming:...'>]
  
In [6]: response.xpath('//title/text()').extract()                              
Out[6]: ['DMOZ - Computers: Programming: Languages: Python: Books']

In [11]: response.xpath('//title/text()').re('(\w+):')                          
Out[11]: ['Computers', 'Programming', 'Languages', 'Python']
```



#### 문법 - 사용법

```
response.css('head > title').get() 
response.css('head > title').getall() # list
response.css('head > title::text').get() # 
response.xpath('//div/ul/li/text()').get() # 
response.css('div.best-list li > a::text').getall(
```



#### 정규표현식

```
response.css('div.best-list li > a::text')[1].re('(\w+)')

response.xpath('//div[@class="best-list"]/ul/li/a/text()')[1].re('(\w+)')
```





### Pipelines - Filtering

아이템이 생성될 때 파이프라인 함수를 한 번씩 거친다고 생가하면 됨!

```python
from scrapy.exceptions import DropItem
class NavernewsPipeline(object):
def process_item(self, item, spider):
print (item)
if item['price'] > 10000:
return item else:
raise DropItem("drop item having lower price than 10000")
```



### dd

```python
    def start_requests(self):
        yield scrapy.Request(url='http://corners.gmarket.co.kr/Bestsellers', callback=self.parse)

```

지정 url 크롤링 후 parse 함수를 call-back ( call-back 으로 부르는 함수는 반드시 response 보유 필수)





### 문제

1. describtion이 전혀 나오지 않는다. 

   `scrapy shell url` 로 만질 때는 아주 잘 나오는데 막상 코드로 넣으면 빈 리스트만 반환한다.  미치겠다... 미치겠다 외 ... 않되? 왜 안 되는지 정말 모르겠다... 짐작은 가는데... 내가 어떻게 만져야하는지 모르겠다... 빵 먹고싶다...

   title:

   //*[@id="site-list-content"]/div[17]/div[3]/a/div

   //*[@id="site-list-content"]/div[18]/div[3]/a/div

   desc:

   //*[@id="site-list-content"]/div[17]/div[3]/div/text()

   //*[@id="site-list-content"]/div[18]/div[3]/div/text()

   

2. 쓰레기값 해결 문제

   ```
   {"title": ["Data Structures and Algorithms with Object-Oriented Design Patterns in Python "], "link": ["http://www.brpreiss.com/books/opus7/html/book.html"], "desc": ["\r\n\t\t\t\r\n                                    The primary goal of this book is to promote object-oriented design using Python and to illustrate the use of the emerging object-oriented design patterns.\r\nA secondary goal of the book is to present mathematical tools just in time. Analysis techniques and proofs are presented as needed and in the proper context.\r\n                                    ", "\r\n                                  "]},
   {"title": [], "link": [], "desc": []},
   
   ```

   1. 값이 정확히 나온 부분의 문제 : desc 리스트 [0]번째 값만 필요함 - 정규표현식을 써야 하는 건가? 근데 리스트 형태라서 strip만 되는 거 같은데... 
   2. 빈 값 처리 - 뭐야! 

   를 해야한다... 

   

### 문제 해결

1. `i.xpath('/div[3]/div/text()').extract()` > `i.xpath('div[3]/div/text()').extract()`

   하~ 진짜 슬래쉬 때문에 개고생 하다니...핳



### 고찰

1. 나는 바보다
2. 눈을 똑바로 뜨자
3. 더 똑똑해지자
4. 컴퓨터는 잘못 없다