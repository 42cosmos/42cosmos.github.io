---
layout: post
title: 'Message Authentication and Op Mode'
tags: [auth, security]
categories: 'Study/Security'
---

\1. 송신자 확인 / 검증 목적 > 보낸이를 확인하기 위해서 2. 메세지의 무결성 

![img](https://k.kakaocdn.net/dn/bgQtVL/btqARyH4zfw/FHymWAxGfRBcYObc0bhAK1/img.png)

MACm=F(Kab, M) 

  Message not altered 

  The alleged sender confirmed 

  The proper sequence of messages assured 

Similar to encryption 

  NIST recommends the use of DES 

  One difference: authentication algorithm need not be reversible, less vulnerable 

메세지 저네를 암호화하는게 아니라 메세지에 대한 조금한 해쉬함수를 만들어서 전송 확인할 때도 해쉬값만 확인



**Hash Function** 

condenses arbitrary message to fixed size > No secret key needed
usually assume hash function is public, hash used to detect changes to message 

통조림 : 데이터가 들어가면 고정된 크기가 생성 > 무엇을 넣던 간 동일한 산출값 

1. 해쉬함수란 ? 

2. 퍼블릭키로 복호화 할 때… 퍼블릭키에 대한 신뢰성 문제?





**one-way property** : computationally infeasible to find data mapping to specific hash 

데이터 입력-해쉬값 출력 / 원본은 찾기 힘들어야 한다는 이론. 
항상 정해진 값 산출로 일방향은 쉬운데 역방향은 불가능

**collision-free property** : computationally infeasible to find two data to same hash

충돌 > 정해진 해쉬값 32글자 해쉬값이 나오게 되어 있다. 운 좋게 같은 해쉬값이 나올 수 있다 입력은 무한 출력은 유한함 . 똑같은 해쉬값을 찾고자 입력 데이터를 만들기는 만들기는 굉장히 힘듦



간단한 특성으로 어디서는 가능함 / 연산이 간단하다고 말하는데, 역으로는 안 됨 > 안전한 특성과 간단한 연산 > 전기를 덜 먹음 > 작은 곳에서도 실행이 가능함 … 가장 간단한 기기에도 들어갈 수 있는 해쉬함수

**Secure Hash Algorithm** - 대표적인 해쉬 함수

키사이즈가 없음 키가 들어가지 않아서 얼마자리 크기의 해쉬 함수를 만들어내는가? 

sha-224 : 해쉬값 크기 | 숫자가 클 수록 컬리젼이 덜 발생함 

\> 역으로 찾을 수 없지는 않지만, 숫자가 커질 수록 경우의 수가 늘어나서 같은 경우를 찾기 힘들어짐 

\> 유한의 범위가 증가

- Designed for compatibility with increased security provided by the AES cipher



**Keyed Hash Functions as MAC** | KeyedHash = Hash(Key | Message) 

 \> led to development of HMAC - 전기들어가는 건 웬만하면 다 할 수 있음

H(M) > h / M, M’ 비교 하지 말고 > 해쉬함수로 돌려서 결과물이 같은지 다른지 확인 H(M) =?= H(M’) > 

h =?= h’ 굳이 100기가 …파일을 확인하지 않아도 32바이트 해쉬값을 찾으면 됨



메세지말고 다른 걸 붙이고 싶어했음 > 키드해쉬값

H(K(키값) || M(메세지값 )) 그냥 키에 메세지를 붙이고 키와 메세지 전체를 해쉬로 돌림 

메세지를 받았을 때, 키를 알아야 하는데 키를 아는 사람만 만들 수 있는 해쉬 키를 모르는 상황에서는 해쉬값을 만들 수 없음 > 메세지 인증 : 메세지 무결성 / 상대 퍼블릭키로 풀린다는 점에서 송신자를 확인할 수 있는 것 



***\* HMAC**

- use, without modifications, hash functions 
- use and handle keys in a simple way. 
- allow for easy replaceability of embedded hash function 
- preserve original performance of hash function without significant degradation 
- have well understood cryptographic analysis of authentication mechanism strength 

![img](https://k.kakaocdn.net/dn/ef9LQI/btqAThezEjO/izn4z08fCHwKpQ31tMckw0/img.png)



**Modes of Operations** - 암호학의 연장선 ( 동작 모드 : 대칭키 암호는 동작모드까지 언급 필수)

block ciphers encrypt fixed size blocks
  eg. DES encrypts 64-bit blocks with 56-bit key 

need some way to en/decrypt arbitrary amounts of data in practise 

NIST SP 800-38A defines 5 modes 

have block and stream modes
to cover a wide variety of applications 

can be used with any block cipher 



- Electronic Codebook Mode (ECB) 
  message is broken into independent blocks which are encrypted 
  each block is a value which is substituted, like a codebook, hence name 
  each block is encoded independently of the other blocks 
    Ci = E(K, Pi) 
  uses: secure transmission of single values 
    message repetitions may show in ciphertext if aligned with message block
    particularly with data such as graphics 
    or with messages that change very little, which become a code-book analysis problem weakness is due to the encrypted message blocks being independent
  main use is sending a few blocks of data

문제 : 패턴이 보임 기본적으로 실루엣이 보임 잘라서 암호화하기 때문에 des8 aes 16 // 8바이트 8글자 그림은 1~2바이트가 점 1개 데이터가 너무 많아서 데이터의 윤곽이 보이는 문제

같은 패턴의 반복이 나오면 그게 보임. 일종의 모드라고는 하는데 모드가 아니고 아무것도 없는 상태라고 봄 

- Cipher Block Chaining Mode (CBC) : 앞 블럭 값을 XOR로 입혀서 재암호화 하는 것* 같은 값을 암호화 해도 앞의 메세지에 따라 달라짐 
  message is broken into blocks
  linked together in encryption operation 
  each previous cipher blocks is chained with current plaintext block, hence name 
  use Initial Vector (IV) to start process 
    Ci = E(K, Pi ⨁ Ci-1)
  C0 = IV 
  uses: bulk data encryption, authentication

피원과 피투가 똑같을 때 실질적으로 암호화 될 때는 피원은 아이브이, 피투는 씨원값의 엑스오알… 암호화가 되니까 계속 같은 값이더라도 앞에서 들어오는 값이 달라지기 때문에 실질적 암호값은 달라짐

계속 같은 값이라도 계속 뒷 암호화에 영향을 주니까 … 다시 말하자면 피원부터 피5까지 다 똑같다고 하더라도,, 값이 계속 바뀜

![img](https://k.kakaocdn.net/dn/buOYv5/btqAQNlEytX/m8Y2P8lr7ss75JjmwUZz31/img.png)



- Cipher Feedback Mode (CFB) 
  message is treated as a stream of bits 
  added to the output of the block cipher 
  result is feed back for next stage (hence name)
  standard allows any number of bit (1,8, 64 or 128 etc) to be fed back 
    denoted CFB-1, CFB-8, CFB-64, CFB-128 etc 
  most efficient to use all bits in block (64 or 128) 
  Ci = Pi ⨁ E(K, Ci-1) 
  C0 = IV 
  uses: stream data encryption, authentication 

문제 > 중간에 하나씩 만들어서 통신으로 보낼 때,데이터는 전송될 때 손실되는 경우가 심함 비올 때 특히 데이터가 많이 날아감.. 전파가 물에 약함 통과를 못함 신호가 가다가 깨지고 등등 한두 개 보내는 게 아니라 만개 십만 개니까… 중간 다섯 번째가 데이터가 손실 되었을 때 ,,, 그럼 복호화 할 대 계속 앞에 게 있어야 함… 5,6이 없으면 그 뒤로 계속 못풂 … 일단 뒤에 걸 다 기다리고 있다가 깨진 부분이 올 때까지 기다려야 함



**Advantages and Limitations of CFB 
**appropriate when data arrives in bits/bytes most common stream mode 

Limitation: need to stall while doing block encryption after every n-bits 

note that the block cipher is used in encryption errors propagate for several blocks after the error 





플레인 택스트를 작게 만들고… 씨비씨처럼 아브이로 시작 암호화된 값을 자르고 그걸 다시 암호

 씨원을 갖고 위로 올려서 집어 넣음 암호화 결과가 작기 때문에 쉬프트 레지스터에 넣음

데이터가 있으면 쉬프트 시킴 /여기서는 레프트. 한 칸 왼쪽으로 밂. 

원래 있던 값이 들어가는 건 CBC와 비슷 



![img](https://k.kakaocdn.net/dn/KP3f2/btqARxWKB9o/OMof3UACklEio7BinQAHK1/img.png)





- Counter Mode (CTR) 
  a “new” mode, though proposed early on 
  similar to OFB bur encrypts counter value rather than any feedback value
  must have a different key & counter value for every plaintext block (never reused) 
  Oi = E(K, i) 
  Ci = Pi ⨁ Oi
  uses: high-speed network encryptions
   

**Advantages and Limitations of CTR** 

efficiency
  can do parallel encryptions in h/w or s/w 

  can preprocess in advance of need 

  good for bursty high speed links 

random access to encrypted data blocks provable security (good as other modes) 

but must ensure never reuse key/counter values, otherwise could break (cf OFB) 



10초후 어떤 데이터가 발생할지 모름. 근데 씨티알은 먼저 계산할 수 있음 점선 안 박스 > 플레인 텍스트를 암호화하는게 아니니까 / 데이터가 올 때마다 게산할 필요가 없어짐 // 통신 측면에서 유리해짐



블럭 사이퍼는 데이터가 어느정도 쌓였을 때 … 양동이 단위로 복호화 /. 스트림은 바로바로

블럭과 스트림의 차이가 애매해지긴 했음 블럭이 작고… 8, 16바이트가 어느정도 된다고 생각했는데 지금은 작고.. 기본적 데이터가 너무너무 커졌음. 예전엔 의미가 있었음.

![img](https://k.kakaocdn.net/dn/cPho0z/btqARXVenaN/AaFtrN6A9xtgdLI71pm0Hk/img.png)