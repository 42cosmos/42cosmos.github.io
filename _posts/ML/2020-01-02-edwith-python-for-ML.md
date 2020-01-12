---
layout: post
title: '[Edwith] 머신러닝을 위한 Python_chap01'
tags: [edwith, ML, python]
categories: 'Study/ML'
---

### News Categorisitaion

숫자를 벡터로 좌표평면상에 올릴 수 있도록 바꾸어주어야 함.

파이썬으로 얘기하면 lmn 이 많은 벡터를 만들고 벡터끼리의 거리를 만들면 됨.

문자 > 숫자 > Vector

One hot Encoding (Bag of Words) 기본적 문서에 대한 벡터 표현

하나의 단어를 벡터로 인식하기 위해서는 벡터 스페이스를 만듦

벡터 스페이스 : 각 글자들이 어떤 인덱스에 포함되는지 정의한 공간
단어별로 인덱스를 부여해 문장에 단어가 몇 개인지 표현

<br/>

### 유사성 판별

##### Euclidian distance

피타고라스 정리, 두 점 사이의 직선 거리

##### cosine distance

두 점 사이의 각도, 데이터셋이 클 수록 잘 나오는 경향 존재

더 많이 사용됨

<br/>

파이썬 폴더끼리 연결 :

os.path.join > 윈도우즈는 역슬래쉬, 리눅스나 맥은 슬래쉬라서 ... 오에스에 맞추어 조인을 해줌

os.sep > os에 따른 구분 기호 (\, /)

<br/>

corpus = 텍스트 워드로 인덱스를 만들어 줌 / 문서의 수 * 단어의 수 = 총 매트릭스의 크기

하나의 문서에 대한 벡터값 단어 수와 같음.

47라인 : 텍스트에서 단어를 뽑고, 단어를 전처리와 똑같은 방식으로 get_cleaned_text함수를 적용 : corpus 딕트 안에 키값을 사용해 이 값의 인덱스를 가져오는 것 == 전처리 방식이 동일해야 함. > corpus[get_cleaned_text(word)] turned to number // 결과값 : 3509 - 첫 번째 문서의 첫 번째 단어가 corpus dict 에 있는 3509 인덱스 값의 문자라는 뜻

```python
word_number_list = [[corpus[get_cleaned_text(word)] for word in words] for words in text]
```

<br/>

48라인 : 매트릭스 생성.

[[0 for _ in range(len(corpus))] for x in range(len(text))]

0을 text의 길이 (=80)에 corpus의 길이 (4032)만큼 2차원 배열로 생성

for의 _(언더바) > 사용하지 않겠다는 의미

```python
X_vector = [[0 for _ in range(len(corpus))] for x in range(len(text))]
```

<br/>

**50 ~ 53 line 이후 미리 만들었던 word number list (*3509,,, 등등)에서 각각의 인덱스에 해당하는 값들을 1씩 올려주면 됨 **

```Python
    for i, text in enumerate(word_number_list):
        for word_number in text:
            X_vector[i][word_number] += 1
    return X_vector
```

전체 corpus 인덱스 번호 별로 어떤 단어가 몇 개 있는지 리스트 형태로 확인 가능

<br/>

#### 비교방법

```python
import math
def get_cosine_similarity(v1,v2):
    "compute cosine similarity of v1 to v2: (v1 dot v2)/{||v1||*||v2||)"
    sumxx, sumxy, sumyy = 0, 0, 0
    for i in range(len(v1)):
        x = v1[i]; y = v2[i]
        sumxx += x*x
        sumyy += y*y
        sumxy += x*y
    return sumxy/math.sqrt(sumxx*sumyy)
```

첫 번째 문서와 두 번째 문서의 유사도를 보여줌

<br/>

#### 비교 결과

```python
def get_similarity_score(X_vector, source):
    source_vector = X_vector[source]
    similarity_list = []
    for target_vector in X_vector:
        similarity_list.append(
            get_cosine_similarity(source_vector, target_vector))
    return similarity_list


def get_top_n_similarity_news(similarity_score, n):
    import operator
    x = {i:v for i, v in enumerate(similarity_score)}
    sorted_x = sorted(x.items(), key=operator.itemgetter(1))

    return list(reversed(sorted_x))[1:n+1]
```

source : 찾고자 하는 문서

similarity_score : 80개의 문서들이 비교 대상 문서와 얼마나 비슷한지 값이 저장됨. (0.6441510... )

similarity_list : 1 개의 문서와 80개의 문서를 비교한 후에 저장되었음

각 문서 번호들마다 얼마나 근접한지 값을 보여줄 것임.

<br/>**get_top_n_similarity_news**  : 키값으로 정렬해서 밸류값 중 가장 큰 값의 인덱스 값을 같이 반환해주는 함 / 가장 유사한 값 10개
