---
layout: post
categories: Linear_Algebra
title: 고유치 eigenvalue 계산 알고리즘 개론
---

### QR Algorithm

보통 사용하는 알고리즘  
행렬 A가 주어졌을 때,  QR decomposition 을 함 Q는 Invertible  
QR decomposition을 토대로 RQ를 만듦 → 새로운 행렬 A1은 A와 similar 한 관계에 놓임  
특정 조건 하에서, Ak는 upper triangular matrix로 수렴하게 됨 또한  A와 Ak의 eigenvalue는 같다.



#### QR 알고리즘에 필요한 QR decomposition

- Gram-Schmidt Process - 최악의 선택 Numerically unstable
- Givens reduction
- Householder method

### Householder method

#### Householder Reflector

$$P=I - 2\mathbf{u}\mathbf{u}^T$$ > u is unit vector  
Identity 매트릭스에 $$2\mathbf{u}\mathbf{u}^T$$ 를 빼준 형태 

$$\mathbb{R}^n$$  스페이스에 있는 임의의 $$\mathbf{x}$$ 를 가정하고, $$P_\mathbf{x} = \mathbf{x} - 2\mathbf{u}\mathbf{u}^T\mathbf{x}$$ 닷프로덕트를 정리해 재정의하면 $$\mathbf{x} - 2(\mathbf{x} \cdot \mathbf{u})\mathbf{u}$$  
이때, $$P\mathbf{x}$$ 의 의미는 X에 하우스홀더 리플렉터를 곱해주면 하이퍼플레인 H 를 통해 반사된 것과 같은 벡터를 만든 것! 



#### HR for QR decomposition

유닛벡터를 담는 방법이 핵심

$$\mathbb{R}^n$$  스페이스에 있는 임의의 $$\mathbf{x}$$ 를 가정하고, $$\rho = \pm1$$ (수치적 오차에 따라 선택되는 사항)  $$\alpha=\rho\parallel x\parallel $$ 일 때  
