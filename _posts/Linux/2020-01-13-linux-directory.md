---
layout: post
title: '디렉토리 구조와 파일 찾는 법'
tags: [inflearn, Linux]
categories: 'Study/Linux'
---

### Directory 구조

디렉토리 : 정리정돈의 수단, 데이터와 실행 프로그램 성격에 따라 정해진 규칙이 있음.

/bin - user binaries : 사용자 사용 명령어 위치

/sbin - System binaries :  시스템 관리 목적이 있는 명령어 위치

/etc - Configuration Files : 설정

/var - Variable Files 

/tmp - Temporary Files 

/home - Home Directories 

/opt - Optional add-on Applications  

/usr - User Programs : 사용자 설치 프로그램은 /usr/bin 에 저장되고, 번들형식으로 사용자에게 제공되는 것들은 /bin에 저장됨



#### locate & find

**locate**는 Directory 가 아니라 DB 안에서 찾기 때문에 훨씬 빠른 반환이 가능함

**find** 는 Directory를 뒤져 찾음. 다양한 사용법이 있음.



#### whereis & $PATH

**whereis** 프로그램

**which** - locate a program file in the user's path



**$PATH** - 환경변수

`echo $PATH` : path 변수에 담겨있는 데이터가 echo를 통해 출력됨. 

e.g. ls 입력 > $PATH에 담겨있는 디렉토리를 검색해서, ls를 존재하는지 찾고 발견 시 실행하는 것

