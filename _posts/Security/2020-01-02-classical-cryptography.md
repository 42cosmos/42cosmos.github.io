---
layout: post
title: 'Claasical Cryptography'
tags: [cryptography, security]
categories: 'Computer_Security'
---



**Caesar Cryptography** : 순서를 조절 

\> Replace a letter into the next of the next - We can express the Caesar encryption algorithm into an equation 

1. Easy to break 2. Only 25 keys 3. Vulnerable to brute force attack encryption 
   E(k(밀어낼 자릿수-형문), p-키) … x,y,z 는 보통 나눈 후 나머지를 차용 e.g. 3을 더한다음에 26으로 나눈 나머지… 
   복호화 D(키, 사이퍼텍스트) 
   쓸 수 있는 키의 경우의 수가 25개 > 쉽게 깨짐



**Single letter substitution** ( 전형적인 암호문 )

- Replace a letter to another 
- 26! keys are possible .. > Calculate the frequency of a letter 

각 글자가 나온 빈도수를 계산 > E, T가 가장 많이 사용됨 > P, Z가 높은 확률로 e, t

많이 나오는 패턴을 분석해 단어를 조합 (the … ) 키가 무조건 많다고 해서 안전한 것은 아님. 



**Playfair** 

\- Multiple-letter encryption ( Create 5x5 matrix based on a given keyword )

![img](https://k.kakaocdn.net/dn/cG0LJu/btqAOb1ygQz/lPAGV2RxtMFdpfIJiPx0Z1/img.png)

**Vernam** ( 지금도 쓰이는 방식 )

\- Use key streams 

xor - 0111  > A O+ B O+ B = A … xor이 두 번 되면 제자리로 돌아옴

​    1010

   ————

​     1101

아이번째 키 O+ 아이번째 플레인 텍스트 = 암호화

E (k, p) = ki O+ pi각각에 대해 xor

![img](https://k.kakaocdn.net/dn/dIo22d/btqAQ4mJoDr/3EWPPewkSivpcG8PJcJUvk/img.png)



**One time pad** 

- Use a key stream that is perfectly random without any repetition 

- One Time Pad provides prefect security 

- Impractical 

- - The size of a key stream should be the same as that of its message

원타임패드~ > 버남 + 부가 조건 > 키 스트림 = 플레인 텍스트

원타임 패드의 조건 = 일회용… + 완벽한 랜덤 … 퍼펙트 시큐리티라는게 도달하기 힘든 뉴스 > 활용성 저하



**Rail fence** 

Transposition



**Rotor Machine** : 현대 컴퓨터로 넘어가기 전에 쓰인 가장 대표적이고 독특한 암호

\- The Enigma machine : Consists of multiple (3) cylinders > 26^3 = 17,576 substitutions 



**Symmetric Cryptography** 

plaintext - original message 

ciphertext - coded message 
cipher - algorithm for transforming plaintext to ciphertext 알고리즘 자체
key - info used in cipher known only to sender/receiver 암복호화 할 때
encipher (encrypt) - converting plaintext to ciphertext 플 > 암
decipher (decrypt) - recovering ciphertext from plaintext 
cryptography - study of encryption principles/methods 암호학
cryptanalysis (codebreaking) - study of principles/ methods of deciphering ciphertext without knowing key 

cryptology - field of both cryptography and cryptanalysis 



**Symmetric Cipher Model** 

대칭 : 가운데를 기준으로 잘라 봤을 때 키가 똑같음. 

대칭 : 키 두개가 대칭이다 > 암호화 할 때랑, 복화하할 때랑 

K의 키가 같으면 대칭키라고 함. 원래 당연시 여겨졌는데, 이게 꼭 두개가 같을 필요가 없다는 말이 생기고는 다양한 기술이 나옴

![img](https://k.kakaocdn.net/dn/GHl5G/btqARh66P5y/7DLWjkwN7aYjxIqznO0a21/img.png)

**Requirements** 

- two requirements for secure use of symmetric encryption: 
- a strong encryption algorithm 
- a secret key known only to sender / receiver mathematically have: 

Y = E(K, X) 

X = D(K, Y)
\- assume encryption algorithm is known implies a secure channel to distribute key



**Cryptography** 

Number of keys 1. Single Key 2. Two Key ( Private and Public )

싱글키 : 우리가 알고있는 대칭키암호, 암호화 복호화가 같아서 하나만 쓰이는 것.

더블키 : 퍼블릭 크립토지만, 암복호화 키가 다름. 이걸로만 암호화하면 이걸로만 복호화할 수 있고…

 요즘 디지털서명, 공인인증서에 사용됨



Plain text processing 1. Block 2. Stream

블럭 : 하나의 묶음 일종의 양동이. 대부분이 블럭 암호화. 용도 : 고정된 데이터 ( 하드디스크, 영화파일, 이메일 _) - 실시간성에서는 안 좋음. 딜레이 발생 

스트림 : 흘러가는 것. 단순하지만 블럭 암호가 발전되어 있고 대중화되어 있음. ( 넷플릭스, 실시간 주고받는 경우 실시간으로 데이터가 생길 때마다 암호화 해야 함. ) 



**Cryptanalysis** 

\- objective to recover key not just message 

\- general approaches: 1. cryptanalytic attack 2. brute-force attack



**How secure?** 

Perfectly secure - Unconditionally secure 

Computationally secure - 비용자체가 (시간 돈 등) 정보 자체의 가치보다 암호문깨는 비용이 더 듦

- The cost of breaking the cipher exceeds the value of information 
- The time required to break the cipher exceeds the lifetime of information 



**Brute Force Search ( Or brute force attack )**

- always possible to simply try every key
- most basic attack, proportional to key size ( 상대적인 경우 ) 
- assume either know / recognise plaintext 

![img](https://k.kakaocdn.net/dn/ErMRa/btqARx2VV2y/HviVvEEm8PYS7qqmpelnI1/img.png)

**Feistel Cipher Structure** 

 \> based on concept of invertible product cipher 

- partitions input block into two halves 
- process through multiple rounds which perform a substitution on left data half
  based on round function of right half & 
  subkey then have permutation swapping halves 

block size: 128 bits 

key size: 128 bits 

number of rounds: 16 subkey generation algorithm 

Round function fast software en/decryption 



장점 : 암호문 생성 이후 복호화 할 때 거꾸로 하면 됨.

\> 구조는 똑같이 사용하면서 키만 거꾸로 넣으면 됨.

F(k, R)만 복잡하게 만들면 됨. 서브키를 16개 만듦 
F박스 함수를 지저분하게 만들면 됨



**Symmetric Block Cipher Algorithms** - 이름 / 특성 / 나오게 된 이유

1. DES (Data Encryption Standard) - 미국 니스트 (표준평가원 등) 
   adopted in 1977 by NBS (now NIST) as FIPS PUB 46
   encrypts 64-bit data using 56-bit key
   대부분의 암호들이 블럭을 64로 하면 키도 64로 하는데 des 는 56을 사용함
   has widespread use / considerable controversy over its security 
   1) Feistel cipher structure 
   2) 56-bit key
   3) Block cipher
   4) 16 rounds 
   5) S-Box for non-linearity 
   \> 완전하게 만드는 방법 > 키 사이즈 늘리기 … 트리플 des 나옴

![img](https://k.kakaocdn.net/dn/GmdoM/btqASzlGczv/iADvaYRuT7esLrLsFFO5n1/img.png)

1. 3DES (Triple DES) 
   \> 트리플은 중간에 암호화 복호화를 한 번 거침
   공학적 해결 방법 : 암호화를 세 번 하는데 중간에 복호화를 함. 일반적으로 암호기법을 칩에다 만들어 침으로 가는 경우가 많음. 그래서 회로로 넣어놓음. 가끔가다가 des를 쓰고싶을 때 키 값을 같은 걸로 줌 > 트리플 디를 쓴 것 처럼 세 번 커짐. 회로를 두 개를 만드느니.. 하나만 만들어서 비용절감을 이룸

2. AES (Advanced Encryption Standard) - 가장 많이 쓰임 
   has 128/192/256 bit keys, 128 bit data 
   \> an iterative rather than feistel cipher : processes data as block of 4 columns of 4 bytes 
   operates on entire data block in every round 
   키 사이즈가 여러가지 > 라운드를 16번 돌면 128, 16+8이면 192… 사용자가 원하는 만큼 … 
   모든 데이터가 256비트가 필요한 건 아니기 때문에. 무조건 안전하게 만드는 게 아니라 계산적 안정을 줌

   Designed to be …
   -1 resistant against known attack
   -2 speed and code compactness on many CPUs
   -3 design simplicity
   initial XOR key material & incomplete last round with fast XOR & table lookup implementation 

구조는 똑같고 돌 때마다 새로운 키가 있어서 변화를 많이 시킴. 페이스탈처럼 단순하지는 않지만 여러번 돌리는 구조는 같음. 라운드를 많이 돌리고 그 때마다 새로운 키를 넣고… 많이 시도하면서 계속 어그러트려서 암호를 만듦. 많이 어그러트리려면 키 사이즈가 늘어나야하고…브루텔 기법을 더이상 사용할 수 없음. 

암호화를 해야한다고 하면 거의 256으로 함. CPU에 보통 이제 박혀있음 너무 많이 쓰기 때문에