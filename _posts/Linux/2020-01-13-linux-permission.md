---
layout: post
title: '권한 permission'
tags: [inflearn, Linux]
categories: 'Study/Linux'
---

### Permission

제어 가능 대상 : user > file and directory에 대한 Read and Write and Excute

**Permission denied** 

-rw-r--r--  1 park-eunbin staff    68 12 22 16:31 test.txt

1. -/rw-/r--/r-- / 

2. 1/ 

3. park-eunbin staff  /  

4. 68 /

5. 12 22 16:31/ 

6. test.txt

<br/>

1. **access mode**
   Type ( 파일 -, 디렉토리 d, 링크 ) / Owners Permission (rw > Read, Write, X-excute)/ Groups Permission/ Other /       
2.   / 
3. Owner Group / 
4. -
5. 생성일
6. 대상 이름



### CHange MODe

`chmod [options] mode[, mode] file1 [file2 ...]`



##### e.g.

`chmod o-r file.type` : other 사용자의 Read 권한 삭제

`chmod o+r file.type` : other 사용자의 Read 권한 부여

`chmod o+w file.type`

`chmod u-r file.type` : 소유자의 Read 권한 삭제



#### Excute

파일 실행 권한

특정 프로그램(해석기, Parser)을 통해 실행하는 것 > 제약 없음. 

##### e.g.

`chmod u+x file.type` : user 실행 권한 부여



#### Directory 

r : 디렉토리 안 파일이나 디렉토리 열람 권한 

w : 디렉토리 내 파일 생성 및 삭제 권한

`chmod -R o+w dir`하부 디렉토리 모두 변경 



#### Octal Modes 

1 - excite only 2 - write only, 4 - read only

`chmod 111 file.type`



####  Class

Reference, Class

u, owner

g, group

o, others

a, all

##### e.g.

`chmod a+w file` : 모든 사용자에게 write 권한 부여

`chmod a=rwx file` : 모든 사용자에게 r,w,x 권한 부여

`chmod a= file` : 모든 권한 삭제 