---
layout: post
title: '머신러닝을 위한 Python 01'
tags: [python]
categories: 'Python'
---

### 1) Pythonic Code

- 파이썬 스타일의 코딩 기법
- 파이썬 특유 문법을 활용해 효율적 코드 표현
- 고급 코드를 작성할 수록 더 많이 요구됨



#### Split & Join

#### Split

: String Type 의 값을 나누어 List 형태로 반환
`.split() ` 괄호 안 기준으로 문자열을 나눔



#### Join

: String List 를 합쳐 하나의 String으로 반환할 때 사용
`''.join(var)`

<br>

### List Comprehension

- 기존 List를 사용해 간단히 다른 List를 만드는 기법
- 포함되는, 포괄적인 List 라는 의미로 사용
- 파이썬에서 가장 많이 사용되는 기법 중 하나
- for + append 보다 빠른 속도



**One Dimentional**

`[i+j for i in case_1 for j in case_2]`



**Two Dimentional**

`[[i+j for i in case_1] for j in case_2]`

<br>

### Enumerate & Zip

#### Enumerate

: List element 추출 시 번호를 붙여 반환
`enumerate(var)`



#### Zip

: 두 개의 list 값을 병렬 추출

`for i, (a, b) in enumerate(zip(list_a, list_b))`

<br>

### Lambda & MapReduce

#### Lambda

: 함수 이름 없이 함수처럼 사용할 수 있는 익명함수, python3 부터 권장하지는 않으나 여전히 많이 쓰임
`f = lambda x, y: x + y`



#### Map Function

: Sequence 자료형 각 element에 동일한 function을 적용

- if filter 사용 가능
- 두 개 이상의 list 에도 적용 가능
- python3 부터 iteration 생성 시 list를 붙여주어야 list 사용 가능
- 실행시점의 값을 생성, 메모리 효율적

```python
ex = [1,2,3,4,5]
f = lambda x: x ** 2 print(list(map(f, ex)))
print(list(map(f, ex)))
```



####  Reduce Function

: map과 달리 list에 똑같은 함수를 적용해서 통합

`from functools import reduce`

<br>

## Asterisk *

: 단순 곱셈, 제곱 연산, 가변 인자 활용 등 다양하게 사용됨

**unpacking a container**

- tuple, dict 등 자료형 내부 값을 unpacking
- 합수 입력값, zip 등을 유용하게 사용 가능

<br>

### Collections

: List, Tuple, Dict에 대한 Python Built-in 확장 자료 구조(모듈)



#### deque

- Stack과 Queue를 지원하는 모듈
- List에 비해 효율적인 자료 저장 방식

```python
from collections import deque
#1
deque_list = deque()
for i in range(5):
    deque_list.append(i)
#2
deque_list.appendleft(10)
```



- rotate, reverse 등 Linked List의 특정을 지원
- 기존 list 형태 함수 모두 지원

```python
deque_list.rotate(2)
deque_list.extend([5, 6, 7])
print(deque(reversed(deque_list)))
```



- 기존 list보다 효율적인 자료구조 제공
- 효율적 메모리 구조로 처리 속도 향상

<br>

#### Ordered Dict

- 데이터를 입력한 순서대로 dict를 반환
- dict type의 값을, value 또는 key 값으로 정렬할 때 사용 가능

`for k, v in OrderedDict(sorted(d.items(), key=lambda t: t[0])).items():`

<br>

#### default Dict

- dict type의 값에 기본 값을 지정해 신규값 생성 시 사용하는 방법

```python
from collections import defaultdict
d = defaultdict(object) # Default Dict 생성
d = defaultdict(lambda: 0) # default값 == 0
```

- 하나의 지문에 각 단어가 몇 개나 있는지 세고 싶을 경우 ?

- Text-mining 접근법 - Vector Space Model

```python
from collections import OrderedDict
word_count = defaultdict(object) # Default dictionary를 생성
word_count = defaultdict(lambda: 0) # Default 값을 0으로 설정

for word in text:
  word_count[word] += 1
for i, v in OrderedDict(sorted(word_count.items(), key=lambda t: t[1],reverse=True)).items():
    print(i, v)
```



#### Counter

: Sequence Type의 data element 의 갯수를 dict 형태로 반환

- Dict type, keyword parameter 등도 모두 처리 가능

```python
from collections import Counter
c = Counter()
c = Counter('gallahad') # 각 알파벳이 몇 번 들어가있는지 확인
c = Counter({'red' : 4, 'blue':2})
c = Counter(reds=4, blue=2)
```



- set 연산 지원

```python
c = Counter(a=4, b=2)
d = Counter(a=1, b=2)
c.subtract(d) # c - d
print(c + d)
print(c & d)
print(c | d)
```



- word counter 기능 제공

<br>

#### named tuple

- tuple 형태로 data 구조체를 저장하는 방법
- 저장되는 data variable을 사전에 지정해서 저장
