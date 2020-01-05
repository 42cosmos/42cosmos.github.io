---
layout: post
title: 'Security Requirements, Attacks and Model for network security'
tags: [cryptography, security]
categories: 'Study/Security'
---



**Security Requirements Triad** 

**CONFIDENTIALLITY** : Preserving authorized restrictions on information access and disclosure, including means for protecting personal privacy and proprietary information. 
\> 기밀성 - 무언가를 보이고 싶지 않을 때 (가장 대표적인 형태)



**INTEGRITY** : Guarding against information modifications or destruction, including ensuring information non-repudiation and authenticity

\> 무결성 - 정보가 허가없이 변경이 되지 않았다는 것. 

e.g ) 10만원을 송금할 때 누군가 100만원으로 고칠 수 없음 > 무결성이 깨짐

**
AVALIABILITY** :Ensuring timely and reliable access to and use of information 
\> 가용성 - 사용자가 사용하려할 때 사용할 수 있는가? 

e.g ) 수강신청, 등의 서버 다운 > 해당 서비스를 받지 못하는 상황

== 아무리 보안이 지켜지더라도 사용하지 못하면 의미 없음 

3가지가 모두 지켜져야 하는 건 아니고 용도에 따라 달라짐. 공고를 냈을 때는 무결성 가용성만,,, 



**Security attacks, mechanisms & services** 

\1. Security Attack
  \- Any action that compromises the security of information 

\2. Security Mechanism 

  \- A process / device that is designed to detect, prevent or Security Service recover from a security attack. 

\3. Security Service 

  \- A service intended to counter security attacks, typically by implementing one or more mechanisms. 

------

![img](https://k.kakaocdn.net/dn/W18D1/btqASz63mOh/cOePQK3YbGtHHDFpKUypxK/img.png)

**Passive attacks** 
\1. 릴리즈 - 내가 공격을 수행하지만 참여하지 않음. 

공격이 수행되고 있지만 특별히 가담하고 있는 것은 아님. 

내가 중간에서 끼어들지 않는 것. 

대표적인 것 : 도청… 바비 앨리스 통신 중 중간에서 내용을 읽음 - 도청은 중간에 가로막거나 끊지 않음 

  \> 패시브 어택 가장 대표적 형태 

\2. 교통량, 통화량 분석 - 트래픽 애널리시스 : 

교통량이 얼마나 되느냐를 분석. 통신 중 내용을 읽을 수 있으면 

도청, but 통신이 진행중이라는 것, 양을 분석하는 것. !! 

트래픽은 일반적으로 암호화가 되어 있어서 내용은 모르지만 

지나가는 데이터의 용량을 보고 언어정도는 분석

ex ) 예전에 911 이후에 아프가니스탄 침공할 때… 침공할까 날짜기 궁금했는데 미국방부 앞에 앉아서 지나가는 피자 트럭의 갯수를 셈.저녁에 피자 트럭이.. 갑자기 피자 트럭이 60~70대로 늘어난다면 ? 그만큼 많은 사람들의 야근 > 무언가 할 일이 있다는 의미….. >>> 트래픽 아날 .. 간접적으로라도 분석이 가능



**Active attacks**

![img](https://k.kakaocdn.net/dn/dhiVPD/btqAQ3gVp1P/A5eAsCBji7Po4nP7WbvrNk/img.png)

\1. 매스커레이드 :: 타인인 척 하는 것

\2. 리플레이 어택 :: 리플레이 ! 재시작 > 한 번 메세지가 가면, 중간자가 갖고 있다가 다시 

발신자에게 보냄; 
전통적으로 문제가 되고 잘 통하는 공격. 
// 밥이 앨리스한테 만 원을 보낸다, 
메세지를 중간에 갖고있다가 그 메세지를 10분 후에 또 보내고 또 보내고…그럼 밥이 앨리스한테 계속 보내는 셈이 됨. 
밥이 앨리스한테 보내는 메세지를 그대로 가져왔기 때문에 서명, 비밀 정보를 그대로 갖고 있음. 완벽히 정리된 정확한 정보임.

![img](https://k.kakaocdn.net/dn/bk4AsR/btqAQOqMjZ5/xIscMgrRYyk0NgsJJTaLsK/img.png)

인증받을 수 있는 정보 함양
 \> 다시 보내니까 받는 입장에서는 구분 불가
 \>> 막을 수 있는 방법. 
\1. 시간을 적어 놓음 (서버 시간을 조정으로 혼란 가중)
\2. 보내는 메세지마다 순서를 매긴다. 

\3. 모디피케이션 - 메세지를 받아서 변경하는 것 
\4. 가용성 - 내가 사용하고 싶을 때 쓰는 것. 

:: 가용성 공격 - 서비스 거부 공격** 

::(Denial Of Service) 도스 공격이라고 부름 

  \> 분산해서 공격하면 디도스
    (Distributed Dinial Of Service)

요즘은 양이 많아지는 추세
막을 수 있는 방법 >> 막기가 힘듦. 가게가 문을 열었는데 손님을 받긴 받았는데 저쪽에서 가짜 요청을 막 보냈는데 진짜와 가짜 요청을 구분해 내기가 힘듦. 



**Model for network security** 

![img](https://k.kakaocdn.net/dn/bLCjx9/btqAQ3BfVLW/uBmWLk7eqlt60z06ugwn91/img.png)

**인포메이션 채널 (인터넷) , 어포넌트 (변조, 날조 등 채널)** 

메세지에 무언가 변화를 주어 메세지를 암호화 해서 보낸다. 씨크릿 인포메이션 : 암호화시 쓰는 키 - 무언가 변조를 하는데 서로 알고 있는 걸로 변화를 줌 > 안전한 메세지로 변경. >> 



특이한 것 : 써드 파티 제3자 - 신뢰할 수 있는 제3자의 도움을 받을 수 있음. 제3자를 통해 수발신자가 통신할 수 있음. 씨크릿 인포메이션에 무얼 집어넣느냐에 따라 달라짐.. 트리플 DES… 신뢰할 수 있는 제3자가 비밀