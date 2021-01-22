---
layout: post
categories: Linear_Algebra
title: Matrix 분류와 적합한 Inverse 알고리즘
---

## 성질로써의 분류

1. Real Matrix 
	1. Symmetric 
		1. Positive definite
		2. Negative definite
		3. Indefinite
	2. Non-Symmetric
	
2. Complex Matrix

   1. Hermitian A = A* 에르미트

      1. Real symmetric 의 성질들이 에르미트에도 적용될 수 있음

      2. Positive definite : $$\mathbf{x}^*A\mathbf{x} > 0$$

   2. Non-Hermitian

### Positive Definite 일 경우

#### Cholesky decomposition 

R(L) => Upper(Lower) triangular matrix

Real Matrix Positive definite → $$A = R^T R = LL^T$$  

Complex Matrix Positive definite → $$A = R^* R = LL^*$$ 

#### LDL decomposition

Tridiagonal 형태에서 적용함 ( 간단한 형태 )

D => Diagonal Matrix

1. $$A = UDU^T = LDL^T$$  
2. $$A = UDU^* = LDL^*$$



### Indefinite

#### Diagonal Pivoting method

D => Block Diagonal Matrix 블럭은 **최대 2 by 2** 형태

1. Block symmetric diangonal : $$A = UDU^T = LDL^T$$  
2. Block Hermitian diangonal : $$A = UDU^* = LDL^*$$ 



### Complex symmetric matrix

>  반드시 에르메트 형태와 구분지어야 함!

주로 나오는 분야 : Boundary integral equations  

**Non-Hermitian Matrix ** Definiteness ? → posi, nega, indef 가 모호해짐 : 일반적으로 정의가 되어있지 않음.

보통 Diagonal Pivoting method 알고리즘을 사용!

$$A = UDU^T = LDL^T$$ 형태의 Decomposition을 사용 : Real symmetric matrix 처럼 풀면 된다.



## 모양으로써의 분류

1. Full Matrix

2. Band Matrix : Band의 일부만 존재하고 나머지는 0으로 채워진 경우 ( Diagonal 부분 제외)

   1. 컴퓨터 언어마다 row/col 접근 방식 속도 차이가 나기 때문에 저장 방식을 고려해야 함

   

> Digital Image Processing, Signal Processing, Cryptography 등의 분야에서 나오는 특수한 Matrix

3. Toepliz matrix : 태각선 항의 값이 모두 동일함, 마이너스 인덱스로 표현

   → Levinson-Durbin recursion $$~n^2$$ > 필요 저장 공간은 컬럼 하나 : 정확도 문제 존재

   → Bareiss algorithm $$~n^2$$ > 풀매트릭스를 저장하는 단점이 있음

   

4. Circulant Matrix : 열의 값이 순환함

   → Circular convolution theorem

   → Discrete Fourier transform

   → Fast Fourier transform $$~nlog(n)$$