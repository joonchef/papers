# Deep Learning

## 원문
http://www.deeplearningbook.org/

## 저자
* Ian Goodfellow 5
* Yoshua Bengio 
* Aaron Courville

## Introduction
 이 책은 세 부분으로 구성된다.
 Part I 기본적인 수학적 도구들과 머신러닝의 컨셉 소개
	- 선형대수, 확률과 정보 이론, 수치해석, 머신러닝기본
 Part II 근본적으로 해결 된 기술인 확립된 딥러닝 알고리즘들에 대한 설명
	- Deep Feedfoward Nets, 정규화, 최적화, CNNs, RNNs, 실제적인 방법론, 어플리케이션
 Part III 미래 딥러닝 연구에서 중요하게 여겨질 것으로 생각되는 좀 더 모험적인 아이디어들에 대한 설명
	- Linear Factor Models, Autoencoders, Representation Learning, Structured Probabilistic Models,
	 Monte Carlo Methods, Inference, Partition Function, Deep Generative Models
 
## Part I: Applied Math and Machine Learning Basics
### Linear Algebra111
#### Scalars, Vectors, Matrices and Tensors
Scalars : 단일 숫자들
Vectors : 숫자들의 배열
Matrices : 숫자들의 2차원 배열
Tensor : 가변 수의 축이있는 일반 그리드에 배열 된 숫자 배열
 http://egloos.zum.com/hanmihye/v/3256824
 http://sdolnote.tistory.com/entry/WhatisTensor
#### Multiplying Matrices and Vectors
 m*n product n*p -> m*p (shape)
 결합법칙 성립, 교환법칙 성립X
 https://ko.wikipedia.org/wiki/%ED%96%89%EB%A0%AC_%EA%B3%B1%EC%85%88 (행렬의 곱셈)
#### Identity and Inverse Matrices
 Identity Matrix : 메인 대각만 1로 채워지고 나머지는 0인 행렬
 Inverse Matrix : 어떤 행렬 A와 곱하면 Identity Matrix가 되는 행렬을 A의 역행렬로 정의
#### Linear Dependence and Span
 http://twlab.tistory.com/24
#### Norms
 L-1 norm : 각 원소의 절대값들의 합
 L-2 norm : 원점으로부터의 유클리디안 거리
 http://taewan.kim/post/norm/
#### Special Kinds of Matrices and Vectors
 Diagonal Matrix : 주대각을 제외한 원소들이 0인 행렬
	벡터 v의 원소들을 주대각 원소로 하는 정사각 Dignoal Matrix를 diag(v)로 씀
	diag(v)x는 v와 x의 아다마르곱과 같음
 Symetric Matrix : 행렬 A가 자신의 전치행렬과 같을 때 A를 Symetric Matrix라고 함
 Unit Vector : 길이가 1인 vector
 Orthogonal Matrix : 행렬 A의 전치행렬과 행렬 A의 역행렬이 같을 때 A를 직교행렬이라 함
	행벡터와 열벡터가 유클리드 공간의 정규직교기저를 이루는 실수 행렬
#### Eigendecomposition (고유값분해)
 http://bskyvision.com/59?category=619292
 http://darkpgmr.tistory.com/105 
#### Singular Value Decomposition (특이값분해)
 http://darkpgmr.tistory.com/106
 http://bskyvision.com/251
#### The Moore-Penrose Pseudoinverse(무어-펜로즈 의사역행렬)
#### The Trace Operator
 https://ko.wikipedia.org/wiki/%EB%8C%80%EA%B0%81%ED%95%A9
#### The Determinant
 https://ko.wikipedia.org/wiki/%ED%96%89%EB%A0%AC%EC%8B%9D
#### Example: Principal Components Analysis
 https://wikidocs.net/7646
 http://darkpgmr.tistory.com/110
 https://ratsgo.github.io/machine%20learning/2017/04/24/PCA/