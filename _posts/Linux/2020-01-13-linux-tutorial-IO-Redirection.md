---
layout: post
title: '리눅스 IO Redirection - Shell & Script'
tags: [inflearn, Linux]
categories: 'Study/Linux'
---

### Linux IO Redirection

---

#### output

출력 방향을 바꾸어 반환시킴- redirections of standard output

`ls -l (1)> result.txt` : 출력 결과를 result.txt 파일에 넣음 / 1 == standard output, 2 == standard error

프로그램 실행 상태 : 프로세스



#### input

file 내 포함되어 있는 걸 입력값을 줄 수 있음

`cat type.txt ` : cat에 type을 인자로 Cmd line arg로 전달함 

`cat < type.txt ` : Standard Input (표준 입력) 으로 들어감



#### append



---

### Shell & Script

---

Shell vs Kernel ( core )

shell 에 명령어 입력 > shell은 해석 후 kernel 에게 전달 > hardware > kernel > shell



#### bash vs zshell

같은 부모를 갖고 있지만 zsh이 더 편리하다는 평가를 받고 있음



#### Shell script

`chmod +x file` > `-rw-r--r--` > `-rwxr-xr-x` : x > excutable

