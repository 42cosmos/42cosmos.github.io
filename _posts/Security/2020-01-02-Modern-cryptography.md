---
layout: post
title: 'Modern Cryptography'
tags: [cryptography, security]
categories: 'Computer_Security'
---

현대 암호 : 컴퓨터가 암호화하고, 데이터가 2진수이며 이것이 암호화 된다



**Public-key Cryptography** 

- probably most significant advance in the 3000 year history of cryptography 
- uses two keys – a public & a private key 
- **asymmetric** since parties are not equal 
- uses clever application of number theoretic concepts to function 
- complements rather than replaces private key crypto 



2개의 키, 암호화 할 때 대칭암호 씨멘틱 암호였는데, 이것은 암호키가 2개. 동시에 생겨남. 

완벽하게 페어, 맞물림. 다른 페어가 존재할 수 없음 

\> 한꺼번에 만들어지기 때문에. 두 개의 키가 특이하게 하나로 암호화, 복호화가 가능. ? 

가장 중요한 특성!! 동시생성, 하나로 암호화 하면 하나로만 복호화가 가능함



이게 가능해진 후로 할 수 있는 일이 많아짐 : 두 개가 생겨서 나누면? 두 개를 다 갖고 있을 필요가 없음. 

특징 중 하나가 a를 갖고 a’를 유추할 수 없음 짐작 불가능. 키를 내놓으면 모든사람에게 보여주고 알려주기 때문에 공개키라고 부름. 그래서 퍼블릭! 나머지 하나는 공개하지 않고 소장 > 개인, 비밀키

비밀키는 보통 개인키라고 부름. 공개와 개인키가 있는데, 공개키는 모두가 알고 개인키는 나만 앎. 공개키로 암호화를 해서 암호화 한다. 이 암호화 된 건. a’만 풀 수 있음. 퍼블릭키로 암호화 해서 보내기만 하면 a’만 볼 수 있기 때문에 더욱 쉬어짐 


**key distribution** – how to have secure communications in general without having to trust a KDC with your key

**digital signatures** – how to verify a message comes intact from the claimed sender : 

\> 프라이빗 키의 암호화


플레인 텍스트 암호화 (상대방 키를 알고 있다는 의미에서 ) 밥이 앨리스한테 보내는데, 앨리스의 퍼블릭 키로 보냄 > 표기할 때는 y = E(k, x) >> X = D(k, y) || k가 같으니까 대칭키



앨리스한테 보낼 때 Y = 아무나 알고 있음 E(PUa, x) >> X = D(PRa, Y) - 앨리스만 알고 있음

**a public-key,** which may be known by anybody, and can be used to encrypt messages, and verify signatures

**a related private-key,** known only to the recipient, used to decrypt messages, and sign ( create ) signatures

 \> those who encrypt messages or verify signatures cannot decrypt messages or create signatures 



모든 사람은 내가 공개한 공개키를 보고 나에게 보내면 됨.!! 인터넷은 암호화통신을 해야하는데, 몇 억명 유저 키를 관리할 수는 없음. 이런 문제를 해결함. 거꾸로 공개키로 암호화하면 내가 안전히 받을 수 있음. 개인키로 암호화하면 퍼블릭 키로 풀 수 있음 > 개인키를 암호화하면 공개키가 있는 아무나가 풀 수 있음. 모두 풀어볼 수 있음. 



 대신 이 것은 개인키로는 나만 암호화 할 수 있기에 받은 사람 입장에서는 공개키로 풀 수 있기 때문에 … ? 이 메세지는 확실한 개인키 (수신인)를 나타내는 효과가 있다 >> 디지털 서명!?!? 신뢰?

![img](https://k.kakaocdn.net/dn/bcmhGR/btqAOdd01dA/kfhZ6ArDwfjK7lVSZ76Kt1/img.png)



신경써야 하는 것 > 공개키가 있는데,,, 내 건지 어떻게 아는지? 공개키를 무언가 뒤집어 씌울 수도 있는데?

 \> 누군가 이게 나의 공개키인지 확인을 해주어야 하는데,, 공개키마다 믿을 수 있는 사람을 확인해주자 해서

 제3자.. 확인을 해줌. 공인인증서…. 

내 퍼블릭 키가 인증을 공공적으로 확인을 받음 국민은행이 이것을 보증합니다 해서 누구한테 들이밀어도 공개키를 뒤져봐도 신뢰 가능



퍼블릭키 문제점 : 느림,, 보통 대칭키보다 1000배 느리고 연산량과 전기가 많이 듦. 좋긴 한데 많이 쓰면 안 좋음

데이터 자체 암호화가 아니라,, AES, DES (빠르고 효율적이고 안전, 키를 따로따로가 문제) 키를 랜덤으로 만든다음 키만 퍼블릭키로 암호화 해서 보내면 상대방은 안전하게 받을 수 있음. 만들어서 주었기 때문에 둘만 알 고 있음 > AES, DES 로 풀면 됨 !! 연산이 많아도 상관은 없음 : 데이터 양이 많으면 무조건 대칭키!! 

키 분배 과정은 처음에 AES, DES로 암호화 해야하기 대문에 필요함



**RSA** - 수학적 특성 사용

\- to encrypt a message M the sender: obtains public key of recipient PU={e,n} 

computes: C = Me mod n, where 0≤M<n 

\- to decrypt the ciphertext C the owner: uses their private key PR={d,n} 

computes: M = Cd mod n 



note that the message M must be smaller than the modulus n (block if needed) 

publish their public encryption key: PU={e,n} 
keep secret private decryption key: PR={d,n} 

안정성이 보장되는 이유 : 소인수분해가 거의 불가능하기 때문에 유추 불가능



암호화 : 메세지이긴 하지만 2진수인 알파벳 한 개 (ex, M) 에 e승을 하고 mod n 를 곱함 = C >> 암호문 

복호화 > C^d * mod n== (M^e) d = M^ed mod n 

프라이빗 키로 먼저 암호화 했을 때 (M^d)e == M^de mod n == M^@(n)+1 mod n = M





\* **RSA Example** 

Select primes: p=17 & q=11 

Calculate n = pq =17 x 11=187 

Calculate ø(n)=(p–1)(q-1)=16x10=160 

Select e: gcd(e,160)=1; choose e=7 

Determine d: de=1 mod 160 and d < 160 Value is d=23 since 23x7=161= 10x160+1 

Publish public key PU={7,187}
Keep secret private key PR={23,187} a

\> asample RSA encryption/decryption is: 

given message M = 88 (nb. 88<187)

encryption: C = 887 mod 187 = 11 

decryption: M = 1123 mod 187 = 88 



**Diffie-Hellman Key Exchange**

![img](https://k.kakaocdn.net/dn/N44He/btqARW2t4YF/KkfEZgRF8wU1eWuO2wGfmk/img.png)

First public-key type scheme proposed / practical method for public exchange of a secret key

: used in a number of commercial products 



a public-key distribution scheme
  cannot be used to exchange an arbitrary message 

  rather it can establish a common key 

  known only to the two participants 

value of key depends on the participants (and their private and public key information) 

\- based on exponentiation in a finite (Galois) field (modulo a prime or a polynomial) - easy 

\- security relies on the difficulty of computing discrete logarithms (similar to factoring) – hard all users agree on global parameters: 

  large prime integer or polynomial q 

  a being a primitive root mod q • 

each user (eg. A) generates their key 

  chooses a secret key (number): X < q

  compute their public key: YA = a^xa mod q 

each user makes public that key Ya



| Alice      | Bob        |
| ---------- | ---------- |
| G          | G          |
| Xa         | Xb         |
| g^Xa mod n | g^Xb mod n |
| (g^Xb)^Xa  | (g^Xa)^Xb  |

shared session key for users A & B is KAB: 

\> if Alice and Bob subsequently communicate, they will have the same key as before, unless they choose new public - key



**Man-in-the-Middle Attack** 

공격에 취약함 : 중간자 공격 

앨리스랑 밥 사이에 서있음. 중간에서 통신을 끊음 > 중간자만의 Xc를 만들어서 앨리스의 g^Xa를 끊고, 나의 g^Xc를 보냄, 반대도 마찬가지

결과는 (g^Xc)^Xa | (g^Xc)^Xb가 되기 때문에 중간에 낀 사람은 양쪽 모두와 통신을 할 수 있지만 서로는 전혀 모름. 

일반적으로는 몇 가지 기능을 넣어서 서로를 확인할 수 있게 함

퍼블릭 키 : 키 익스체인지 - 동등한 정보를 나눠가질 때 > 맨인더미들 어택이랑 연결됨





**Digital Signature** E(PrivateR, H)

have looked at message authentication > but does not address issues of lack of trust 

digital signatures provide the ability to: 

  \- verify author, date & time of signature 

  \- authenticate message contents 

  \- be verified by third parties to resolve disputes 

hence include authentication function with additional capabilities 





![img](https://k.kakaocdn.net/dn/bkxvY1/btqARwQudYv/xaCjv6BKviL3aZ7WtCQqKk/img.png)

![img](https://k.kakaocdn.net/dn/cd2p5b/btqAOIY9MI7/RMsxM1WmpgMSQIPExU9SqK/img.png)