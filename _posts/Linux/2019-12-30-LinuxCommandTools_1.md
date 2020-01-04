---
layout: post
title: 'Linux Command Line Tools - 텍스트 처리'
tags: [CLI]
categories: 'Study/Linux'
---

# Linux Command Line Tools



### head 

문서 내용 앞 부분 출력 

파라미터를 주지 않으면 앞 10줄 출력 

##### 자주 사용되는 옵션

- -c, --bytes  # num byte만 출력
- -n, --lines  # num line 만 출력

##### e.g.

- head 'file.type'
- head -n 'num' 'file.type'
- cat 'file.type' | head -n 'num'



### tail

문서 내용 뒷 부분 출력

파라미터를 주지 않으면 끝 10줄 출력 

##### 자주 사용되는 옵션

- -c, --bytes = [+]NUM # print num byte
- -n, --lines = [+]NUM # print num line 
- **-f**, --follow[={name | desc}] # 추가되는 내용 대기하다가, 추가 내용은 append 후 출력 
- -F # truncate > Re-Open > Follow ( using log rotate file )) # 파일이 지워졌다가 생겨도 따라감

##### e.g.

- +5 = 5번째 줄 부터 끝까지 출력

- tail -n 'num' 'file.type' # 뒤에서 'num'번째 줄 출력
- cat 'file.type' | tail -n 'num' # 상동



### WC (Word Count)

line/word/byte count 출력

라인의 수가 특정 목적을 가진 정보 수가 되는 경우

##### 자주 사용되는 옵션

- -l # 라인수만 출력

##### e.g.

- wc 'file.type' == wc -clmw 'file.type'  # line	word	byte count	'file.type'
- wc *.py # 폴더 내 py파일 모두 확인
- wc -l 'file.type' # line 수 
- wc -l 'file.type' | awk '{print $1}'



### nl

파일 내용을 라인 넘버와 함께 출력

코드 첨부 후 설명할 때 유용함 ?

##### 자주 사용되는 옵션

- -ba # 모든 라인 넘버링
- -v N # 시작 라인 넘버를 N으로 지정
- -s # 라인 넘버 출력 후 출력할 separator 지정

##### e.g.

- nl 'file.type' == cat 'file.type' | nl
- nl -ba 'file.type'
- nl -ba -s ":\t" 'file.type'



### sort

*맥은 모르겠다*

파일 내용 정렬 후 출력

##### 자주 사용되는 옵션

1. 위치 지정
   + -k, --key=KEYDEF # key에 의한 정렬, 어떤 컬럼을 기준으로 정렬할 건지 /
     - 숫자 한 개만 작성하면 그 부분부터 끝까지
     - 한 개의 열만 하려면 쉼표로 구분해 같은 숫자 넣어주기
     - n 번째 우선순위 지정 > -k 5,5 -k 2,2 
     - e.g. ls -al | sort -k 5 -n
   + -t, --field-separator # 필드 구분자 (기본값 = 공백), 하나의 기준으로 컬럼을 나누어줌 
2. 정렬 기준 (sort 'file' -x)
   + -f, --ignore-case 
   + -g, --general-numeric-sort
   + -n, --numeric-sort # 123보다 91이 먼저 나오게 됨
   + -r, --reverse # 내림차순 정렬
   + -u, --unique # 중복 삭제
3. 옵션
   + --debug #어디 기준으로 정렬했는지 가시화

##### e.g.

- cat 'file.type' | sort
- cat 'file..type' | sort -t'구분자' -k '정렬키-행' -n 
- cat 'file..type' | sort -t'구분자' -k '정렬키-행' -n -debug



### uniq

중복 내용 제거 후 출력

연달아 중복인 부분만 삭제 >> sort 명령어랑 같이 사용

#### 자주 사용되는 옵션

+ -d, --repeated # 중복된 내용만 출력
+ -u, --unique # 중복되지 않은 내용만 출력
+ -i, --ignore-case # 대소문자 무시

#### e.g.

+ cat 'file.type' | uniq | nl -ba # 중복된 내용만 코드 번호를 붙여서 출력

+ sort 'file.type' | uniq | nl -ba 
+ grep "search" file | awk -F: ''{print $1}' | uniq



### cut

컬럼 잘라내기

#### 자주 사용되는 옵션

+ -b, --bytes=LIST # byte 선택
+ -c, --characters=LIST # character 선택
+ **-f,** --fields=LIST # 필드(컬럼) 선택
+ **-d**, --delimiter=DELIM # tab 대신 사용할 구분자 지정
  탭이 아닌 다른 구분자로 지정되어있는 경우 반드시 입력
+ --complement # 선택 반전
+ --output-delimiter=STRING # 출력시 사용할 구분자 지정

#### e.g.

+ head 'file.type' | cut -d: -f 1, 7 --output-delimiter=">" # 딜리미터 변경

+ ls -al | head | cut -b 1 #각 줄의 첫 글자만 나옴 
+ ls -al | head | cut -b 2-4 # rwx.. 등 권한을 볼 수 있음
+ ls -al | head | cut -b -10 # 처음부터 10바이트까지
+ ls -al | head | cut -b 11- # 11부터 끝 바이트까지



### tr (translate)

내용 변환

문서 특수 캐릭터 삭제 시에 자주 사용

tr [OPTION] ... SET 1 [SET 2]

#### 자주 사용되는 옵션

+ -c, -C, --complement
+ -d, --delete
+ SET
  + CHAR1 - CHAR2 # char1부터 char2까지 (a to z)
  + [:alnum:] # 문자 + 숫자
  + [:alpha:] # 문자
  + [:blank:] # 공백
  + [:space:] # 공백 + newline
  + [:digit:] / [:xdigit:] # 10진수 숫자 / 16진수 숫자
  + [:lower:] / [:upper:] 

#### e.g.

+ tr -d SET1 # set1에 맞는 부분 삭제 후 지워지지 않는 것들 출력
+ cat 'file.type' | tr ':' '%'
+ head 'file.type' | tr [:lower:] [:upper:] # 출력될 모든 소문자를 대문자로 변경



### sed

stream editor

파일 내용을 출력 전에 옵션대로 편집 후 출력



#### 자주 사용되는 옵션

+ {RANGE}p # range 내 라인 출력
+ {RANGE}d # range 내 라인 삭제
+ /SEARCHPATTERN/p # SEARCHPATTERN과 매치되는 라인 출력
+ /SEARCHPATTERN/d # SEARCHPATTERN과 매치되는 라인 삭제
+ s/REGEX/REPLACE # REGEX 매치 부분을 REPLACE로 교체 -substitute
+ -n # 기본 출력 부분 제외 - 보통 print 시 많이 사용
+ '/,+num p'  # 상대적으로 몇 번째 줄까지 출력 할 건지

#### e.g.

+ head 'file.type' | sed '2,5p' # head 부분 출력 + 라인 사이에 sed 옵션이 들어가게 됨
+ head 'file.type' | sed -n '2,5p' # 기본 출력 부분 제외
+ head 'file.type' | sed '1,5d'
+ cat 'file.type' | sed -n '/kwarg/p'
+ cat 'file.type' | sed 's/:/$/g' # g 옵션 : 한 라인에 매치되는 모든 부분을 변경
+ cat 'file.type' | sed -n '/kwarg/,10p' # 검색 문자에서 10번째까지 출력
+ cat 'file.type' | sed -n '/kwarg/,+2p' # 검색 문자부터 2번째 줄을 더 출력



### awk

유틸리티라기 보다는 텍스트 처리 script language

syntax : awk options 'selection _criteria {action }' input-file

파일 내용을 처리하는 거기에 input_file 이 필요하지만, 파이프를 통해 호출하는 경우는 input_file 없음

#### 자주 사용되는 옵션

+ -F # Field separator 지정 

#### 주요 내장 변수

+ $1, $2, $3 # Nth field. wc할 때 awk field separator를 공백으로 해서 $1, $2... 
+ NR # number of records
+ NF # number of fields
+ FS # field separator (default 'white space')
+ RS # record separator (default 'new line')
+ OFS # Output Field Separator
+ ORS # Output Record Separator



#### e.g.

+ wc 'file.type' | awk '{print $1}' # 첫 번째 부분 출력
+ head 'file.type' | awk -Fs '{print $1}'
+ head 'file.type' | awk -Fs '/kwarg/ {print}' # 검색 후 라인 전체 출력
+ head 'file.type' | awk -Fs '/kwarg/ {print NR, $1 }'  # 검색 인자가 몇 번째 라인인지 출력
+ head 'file.type' | awk -Fs '{print NR "==>" $1 }' 
+ head 'file.type' | awk -Fs '{print NR "==>" $1, NF }' # 필드가 몇 개인지 알려줌, 언어라서 loop 도 돌 수 있음.



### 사담

우분투 영상에서 `ls -al | sort -k 5` 는 숫자로 인식하지 않아서 -n을 붙여줘야 했는데, 맥은 아닌가보다...