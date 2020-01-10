---
layout: post
title: 'Foundation for analytics with python - 1'
tags: [python]
categories: 'Study/Python'
---

# pandas

`astype(type)`

`loc[[행], [열]]` - 라벨 값을 기반으로 행 데이터 읽기
e.g. ) data_frame.loc[data_frame['Invoice Number'].str.startswith('920-'), :]

`iloc[[행], [열]]` - 인덱스 값을 기반으로 단일 행을 선택해 열 헤더 행으로 사용할 수 있게 함

`.ix[]` > `loc` 과 같으나 경고 메세지 반환

':' > 모든 행

---

`.columns` - 열 출력
e.g.) data_frame.columns = data_frame.iloc[0] 

`.index` - 행 출력

---

`.contains()` - 특정 문자열 포함 요소 탐색
e.g.) data_frame['Supplier Name'].str.contains('Z'))

`.isin()` - 특정 값의 포함 여부를 확인 후 boolean 타입으로 반환

`.startswith('')` - 특정 문자열로 시작되는 요소 탐색

`.endswith('')` -  특정 문자열로 끝나는 요소 탐색

---

`.reindex()` 

`drop()` - 제거

`read_csv(header = None, names = list_V)`

`concat(axis=0)`- 0 = 수평 / 1 = 수직으로 합침

> `merge()` > `pandas.merge(DataFrame1, DataFrame2, on='key', how='inner')`
>
> Numpy > `numpy.concatenate([array1, array2], axis=1)`
>
> `numpy.hstack((array1, array2))`
>
> `numpy.c[array1, array2]`

<br/>

<br/>

## Errors

```ValueError: illegal newline value:
with open(input_file, 'r', newline=' ') as csv_in_file:
```

1. ValueError: illegal newline value:
   `newline=' '` > `newline=''`  으로 변경하니 오류 해결!

2. modulenotfounderror no module named 'pandas'

   > 가상환경을 열어서 pandas 설치하고 지웠다가 다시 설치하고 컴퓨터 재부팅하고 막... 오만가지 난리를 펼치다가... 터미널 창에서 `which python3` 입력해서 나오는 주소를 py 파일 라인 1에 붙여넣고 실행하니 오류 해결!

   `#! /Users/park-eunbin/miniconda3/envs/IP/bin/python3`

   <br/>

3. b'Skipping line 13: expected 5 fields, saw 7\n' > `data_frame = pd.read_csv(input_file, error_bad_lines=False, warn_bad_lines=False)`
4.  pandas `.ix[]` Message

```
.ix is deprecated. Please use

.loc for label based indexing or

.iloc for positional indexing
```

5. `delimiter =','` 오류 > 해결 못함... 왜? 왜 $1,600.60을 제대로 못걸러내냐ㅜ,ㅠ
6. `.drop`