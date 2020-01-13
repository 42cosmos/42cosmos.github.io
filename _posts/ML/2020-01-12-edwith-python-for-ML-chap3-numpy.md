---
]layout: post
title: '[Edwith] 머신러닝을 위한 Python_chap03 - Numpy'
tags: [edwith, ML, python, Numpy]
categories: 'Study/ML'
---

### Numpy
---
파이썬 과학 처리 패키지 - Numerical Python

- **반복문 없이 데이터 배열 처리 지원**
- C, C++, 포트란
- Dymanic typing 불허


### Array creation

#### ndarray

```python
type(test_array[0])
numpy.float64 # 64는 크기
```

파이썬 : 메모리 주소의 위치를 잡음. 리스트 안에 값이 아닌 메모리 주소 > 복사 == 메모리주소 복사

> `from copy import deepcopy` 로 해결

넘파이 : 차례데로 데이터를 쌓음 > 빠른 데이터 처리가 가능



```python
t = np.array([1,2,3,4], float)
t.shape
# Expected Result - Vector
(4,) # 4 column

t2 = np.array([[1,2,3,4]], float)
t2.shape
# Expected Result - Matrix
(1, 4) # 1 by 4 1 row 4 columns
```

- shape : numpy array의 object의 dimension 구성을 반환함 > 튜플타입 반환
  메트릭스 크기를 따라감
- ndim - # of dimension
- size - data의 개수 : *scala 값이기 때문에 int로 반환*
- dtype : numpy array의 데이터 type을 반환함
  대부분 float32, 64 로 선언 - 메모리에 크기가 결정되기 때문에 신경써야 함

<br/>

### Handling Shape

: Array Shape 의 크리 변경

#### Reshape

Matrix를 Vector로 펴야할 때

\* 데이터 사이즈 개수만 맞추면 됨

```python
np.array(test_matrix).reshape(2,2,2)
np.array(test_matrix).reshape(-1, 2) # -1 : size를 기반으로 row 개수 선정 | row 의 개수는 정확하게 모르지만 컬럼을 2개로 할 때

test = np.array(t).reshape(8,)
# array([1,2,3,4,1,2,5,8])
test.reshape([-1, 1])
# array([[1],[2], ..., [8]])
```

데이터 호출 시 y값을 가져올 때, 이 값이 보통 Vector형태로 뽑히는데, Sklearn에서는 Matrix 형태로 들어가야 하기 때문에



#### flatten

: 다차원 array를 1차원으로 변환

딥러닝 초기모델 배울 때 nlist데이터셋을 쓰는데 ( 문자를 벡터형태를 사용 ), 28 by 28을 펴야할 때...

<br/>

### Indexing & slicing

#### indexing

a[0,0] == a\[0][0]



#### slicing

x:y:z | x : 시작, y : 끝 지점 바로 앞, z : step

- 데이터 일부분만 가져올 때 사용

- List와 달리 **행과 열** 부분을 나눠서 slicing이 가능함 / [행, 열]

- Matrix의 부분 집합을 추출할 때 유용함



### Creation Function

#### arange 

: array 범위를 지정해 값의 list를 생성하는 명령어

- floating point 로도 표기 가능 

```python
np.arange(30)
# array([0,1,2, ..., 29])
np.arange(0, 5, 0.5).tolist()
np.arange(30).reshape(-1,5) # 2차원 매트릭스 형태 생성
```



#### ones, zeros and empty

`np.zeros(shape, dtype, order)` 

: ones, zeros > 1 (0)으로 찬 ndarray 생성

: empty - shape만 주어지고 비어있는 ndarray 생성 **memory initialisation** 이 되지 않음

```python
np.zeros(shape=(10,), dtype=np.int8)
np.zeros((2,5)) 
```

 

#### Something like

: 기존 ndarray shape 크기만큼 1, 0 또는 empty array 반환



#### identity 

: 단위행렬 (i 행렬) 생성



#### eye 

: 대각선이 1인 생렬, k값의 시작 index 변경 가능

```python
np.eye(N=3, M=5, dtype=np.int8) # 3 by 5
np.eye(3,5, k=2) # k == start index > 첫 행의 3번째부터 시작
```



#### diag

: 대각선 값 추출

```python
matrix = np.arange(9).reshape(3,3)
np.diag(matrix) # array([0, 4, 8])
np.diag(matrix, k = 1 # k == start index
```



#### random sampling

: 데이터 분포에 따른 sampling으로 array 생성

```python
np.random.uniform(0, 1, 10).reshape(2, 5) # 균등분포
np.random.normal(0, 1, 10).reshape(2, 5) # 정규분포 
```



### operation functions

#### sum

: ndarray의 element 



#### axis

: 모든 op function 을 실행할 때, 기준이 되는 dimension 축

- [row] : axis = 0> [column, row] : axis = 0, 1 > [num, column, row] : axis = 0, 1, 2

```
np.t_array.sum()
np.t_array.sum(axis = 0)
```



#### mean & std

: 평균과 표준편차 반환



#### concatenate

- vstack : 축 기준 합 > 2차원 배열로 변환
- hstack : 



### array operations

#### operations b/t arrays

: Numpy는 array간의 기본적 사칙연산을 지원



#### Dot product



#### transpose



#### * broadcasting 

: Shape 이 다른 배열 간 연산을 지원하는 기능, 방식

- scalar - vector (matrix) 외에도 vector - matrix 간 연산도 지원



#### Numpy performance

numpy는 concat 시에 느려짐, List가 더 빠름



### Comparisons

#### All and Any

: Array의 데이터 전부(and) 또는 일부(or)가 조건에 만족 여부 반환

- 일종의 broadcasting ( scalar - numpy)

- all : 모두 만족 시 True  / `np.all(a < 10)`
- any : 하나라도 만족 시 False / `np.any(a < 0)` 



#### Logical_operations

`.logical_and(x < 1, y > 1)`, `.logical_not(x)`, `.logical_or(x, y)`



#### * np.where

: 조건에 만족하는 인덱스 값을 반환

- condition을 넣어 T,F 반환도 가능
- 정렬 기법이랑 함께 쓰면 유용함

```python
np.where(a > 0, 3, 2) # True - 3, False - 2
# array([3, 3, 2])
np.where(a>0) # index 값 반환
(array([0, 1]),)
```



#### * argmax & argmin

: return of max(min) of arguments' index / `np.argmax(a)`

- 각 조건에 맞는 값을 찾을 때는 where 절을 사용하면 됨.
- 축을 넣어주면 축에서 최대, 최소값을 찾음 / `np.argmax(a, axis = 1)`



### boolean & fancy index

#### boolean index

- numpy는 배열 특정 조건에 따른 값을 배열 형태로 추출 가능함

- Comparision operation 함수 사용 가능

- 조건이 True 인 index element 만 추출
- where 절과 함께 사용 시 유용
- 데이터 셋에서 조건에 만족하는 값만 찾을 때 > 조건을 변수에 할당 > .astype(np.int) 로 1, 0 변환

```python
test_array = np.array([1, 4, 0, 2, 3, 8, 9, 7], float)
test_array > 3
# array([False,  True, False, False, False,  True,  True,  True], dtype=bool)

test_array[test_array > 3] # array([ 4.,  8.,  9.,  7.])

condition = test_array < 3 
test_array[condition] # array([ 1.,  0.,  2.])
```





#### fancy index

: numpy는 array를 index value로 사용해서 값을 추출하는 방법

- 인덱스에 해당하는 값을 추출함 
- `a[b]` 보다 `a.take(b)` 를 권장 - 명확함

```python
a = np.array([[1, 4], [9, 16]], float)
b = np.array([0, 0, 1, 1, 0], int)
c = np.array([0, 1, 1, 1, 1], int)
a[b,c] # b를 row index, c를 column index로 변환하여 표시함
# array([  1.,   4.,  16.,  16.,   4.])

a = np.array([[1, 4], [9, 16]], float)
a[b]
# array([[  1.,   4.],
#       [  1.,   4.],
#       [  9.,  16.],
#       [  9.,  16.],
#       [  1.,   4.]])
```





### numpy data i/o

#### loadtxt & savetxt

: Text type의 데이터를 읽고, 저장하는 기능



#### numpy object - npy

: 파이썬 객체 저장방식인 pickle 형태로 저장 - binary 파일 형태

