---
layout: post
title: 'Linux Command Line Tools - 검색'
tags: [CLI]
categories: 'Linux'
---


### find

이름이나 속성 등의 조건에 맞는 파일을 찾아 명령 수행

**find [OPTION] path EXPR**

#### 자주 사용되는 옵션

**조건**

- -name # 이름 검색, 가장 많이 사용
- -regex # regex에 매치로 검색
- -empty # 빈 디렉토리 혹은 빈 파일 검색
- -size # 사이즈 검색 (M, G 표기 가능)
  - -N # 이하
  - +N # 이상
- -perm # 퍼미션 검색
  - mode # 정확히 일치하는 파일
  - +mode # 모든 flag가 포함된 파일
  - /mode # 어떤 flag라도 포함된 파일
- -type # 파일 타입 검색
  - d # directory
  - p # named pipe
  - f # regular file
  - l # softdrink
  - s # socket

**액션**

- -delete # 파일 삭제
- -ls # ls -dils 명령 수행
- -print # 파일 이름 출력
- -printf # 파일 이름을 포맷에 맞게 출력
- **-exec** # 주어진 명령 수행
- **-execdir** # 해당 디렉토리로 이동하여 명령 실행
- **-ok** # 사용자 확인 후 exec
- **-okdir** # 사용자 확인 후 실행 execdir

#### e.g.

- find . -name "*.py" # 현재 디렉토리에서 py 파일 찾기
- find . -regextype egrep -regex '.\*hash.*.py$' # $ 파일의 끝을 명시함. hash 앞뒤로 글이 있는 py 파일
- find . -empty
- find . -type
- find . -perm 0644 | wc -l
- find . -perm /u+x  # owner 실행권한이 포함된 파일을 출력 / find: -perm: /u+x: illegal mode string

+ find . -perm /001 -ls # -perm: /001: illegal mode string

+ find . -name -exec {} \;
+ find . -name -execdir {} \;
+ find . -name -ok rm -f {} \; # 안전하게 파일 삭제 가능



### grep

파일 내용 중 원하는 내용 찾기

grep [**OPTION**] PATTERN [FILE...]

#### 자주 사용되는 옵션

+ **-r** # recursive
+ -i # ignore case
+ **-v** # invert match # 패턴과 매치가 되지 않는 걸 찾음
+ -q # quiet mode # 성공.실패만 판단하고 싶을 때

#### e.g.

+ grep PATTERN *.py # py 파일에 PATTERN 이 포함된 걸 찾아라
+ grep PATTERN *.py | awk -F: '{print $1}' | sort -u # 패턴이 들어있는 파일 검색 후 awk 명령어로 파일 이름 분류 후 sort로 unique 한 것만 출력

+ echo $? # 최근에 실행된 명령어, 함수, 스크립트 자식의 종료 상태 / 0 = 성공
+ grep "\\<for\\>" *.py # 단어단위 검색



### apropos

man page 이름과 설명 검색

#### 자주 사용되는 옵션

+ -s, --sections=LIST, --section=LIST # ㅌ탐색할 섹션을 으로 구분하여 입력
+ 1 : 일반적 툴
+ 2 : 시스템 콜
+ 3 : 라이브러리 함수
+ 7 : Overview 등의 개념

#### e.g.

+ apropos print
+ apropos pthread
+ apropos pthread -s 7
+ apropos '^sem_'
+ apropos '.*'
+ apropos '.*' -s 5:6:7



### locate

파일 위치를 보여줌

단, updateddb가 저장해놓은 DB파일 내에서 검색하므로 누락 파일 존재 가능

updateddb : os 레벨에서 정기적으로 업데이트 함

어떤 파일이든 찾아서 보임

**locate [OPTION]... PATTERN**

#### 자주 사용되는 옵션

+ -i, --ignore-case
+ -l, -limit, -n LIMIT
+ --regex



#### e.g.

+ locate main.c -n 10 #



### which

**실행 파일**의 위치를 알려줌 > 일반적인 파일은 불가능

#### e.g.

+ which ls
+ which chmod
+ which ls strace chmod
+ which ifconfig
