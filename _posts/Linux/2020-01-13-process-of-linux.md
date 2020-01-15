---
layout: post
title: '프로세스 & 실행'
tags: [inflearn, Linux]
categories: 'Study/Linux'
---

#### Daemon

특성 

- 항상 실행되고 있음
- server 같은 프로그램
- 언제 클라이언트가 접속할지 모름 > web server > daemon, service라 지칭



#### Service와 자동실행

`sudo service program start/stop`

데몬으로 사용되는, 서비스를 통해 켜고 끄는 프로그램은 start과 stop 2 개의 명령어를 필수적으로 갖고 있음 - /etc/rc3.d

`S02apache2` 링크 ( 윈도우의 바로가기 )

S : 부팅 시 자동 실행

K : kill - 프로그램 실행 X

숫자 : 우선순위

<br>

### Cron

정기적으로 명령을 실행시켜주는 소프트웨어 

`crontab -e`

\# m h dom mon dow    command

\# minutes, hours, day of month, month, day of week, 명령어

e.g. */1 * * * * date >> date.log 2(Standard Error) > &1(Standard Output)



#### Shell startup script

쉘 시작 시 특정 명령어를 자동으로 실행하는 방법

`vi .~/zshrc ` 에 삽입

단축어 만들기 : `alias cmd = 'nick'`