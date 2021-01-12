---
layout: post
title: 'Group - 파일과 디렉토리 공동 관리'
tags: [inflearn, Linux]
categories: 'Linux'
---

### Group

file 생성자 (유저) 외에 한 명 이상의 사용자에게 권한 부여 

`/var` 아래에 공용 directory 생성

1. `sudo groupadd developer`
2.  `sudo usermon -a -G group_name user_name`   
3. exit 후 재접속
4. `sudo chown {-R} [user]{:group} file` 형식으로 입력 



