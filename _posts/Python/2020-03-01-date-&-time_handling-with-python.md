---
layout: post
title: 'date & time handling in python'
tags: [date, time]
categories: 'Python'
---

[데이터 사이언스 스쿨](https://datascienceschool.net/view-notebook/465066ac92ef4da3b0aba32f76d9750a/)



### datetime package

`import datetime`  

1. 날짜 및 시간 == `datetime`
2. 날짜 == `data`
3. 시간 ==`time`
4. 시간 '구간' 정보 == `timedelta`



#### Class

#### datetime

**Attributes**

- `year`
- `month`
- `day`
- `hour`
- `minute`
- `second`
- `microsecond`



**Methods**

- `weekday()` : 요일 반환 (0: 월 ~ 6:일)
- `strftime()` : 문자열 반환
- `strptime()` : 첫 번째 인수 - 날짜 및 시간, 두 번째 인수 - 문자열 해독 형식
- `date()`
- `time()`



**날짜 및 시간 지정 문자열**

- `%Y` : 앞 빈자리를 0으로 채움
- `%m  ` : 상동
- `%d`
- `%H`
- `%M`
- `%S`
- `%A` : 영문 요일 문자열
- `%B` : 영문 월 문자열

```python
dt = datetime.datetime.now()
# datetime.datetime(2020, 03, 01, 1, 26, 55, 731039)
dt.strftime("%A %d. %B %Y")
# 'Sunday 01. March 2020'

datetime.datetime.strptime('2020-03-01 20:45', "%Y-%m-%d %H:%M")
```



### dateutil package

`strptime()` > Use `parse`  in `dateutil`

```python
from dateutil.parser import parse

parse('2020-03-01')
# datetime.datetime(2020, 3, 01, 0, 0)
parse('6/7/2016')
# datetime.datetime(2016, 6, 07, 0, 0)
# 미국식 
```



#### timedelta Class

날짜 혹은 시간의 간격을 구할 때 > `datetime.datetime` 클래스 객체의 차이를 구함 >  return `datetime.timedelta`



**Attributes**

- `days`
- `seconds`
- `microseconds`

**Methods**

- `total_seconds()` : All Attr turns to seconds

```python
dt1 = datetime.datetime(2016, 2, 19, 14)
dt2 = datetime.datetime(2016, 1, 2, 13)
td = dt1 - dt2
td # datetime.timedelta(48, 3600)
```



`datetime.datetime` 클래스 객체 + `datetime.timedelta` 클래스 객체를 더해 새로운 시간을 구할 수 있다

```python
t0 = datetime.datetime(2018, 9, 1, 13)
d = datetime.timedelta(days=90, seconds=3600)
t0 + d # datetime.datetime(2018, 11, 30, 14, 0)
```

