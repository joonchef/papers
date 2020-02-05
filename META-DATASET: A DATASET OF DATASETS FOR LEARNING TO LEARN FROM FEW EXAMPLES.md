# META-DATASET: A DATASET OF DATASETS FOR LEARNING TO LEARN FROM FEW EXAMPLES

## 원문
https://arxiv.org/pdf/1903.03096.pdf

## 저자
Eleni Triantafillou∗†, Tyler Zhu†, Vincent Dumoulin†, Pascal Lamblin†, Utku Evci†, Kelvin Xu‡†, Ross Goroshin†, Carles Gelada†, Kevin Swersky†, Pierre-Antoine Manzagol† & Hugo Larochelle†

∗University of Toronto and Vector Institute, †Google AI, ‡University of California, Berkeley

## Abstract
메타러닝(Few-shot classification)에 활용할 수 있는 데이터셋들을 모아 메타데이터셋을 만들고 알려진 방법론들에 대한 벤치마크 테스트를 수행 및 새로운 방법 제안


## Introduction

인간은 Few-shot learning이 가능하지만 기계학습은 여전히 부족함  
이러한 부분이 개선 되면 많은 데이터가 필요하지 않고 유연하게 지식을 확장 가능한 효율적인 알고리즘이 될 수 있음  
배우는 방법을 학습함으로써(meta-learning) few-shot learning을 구현 할 수 있을 것

기존 벤치마크인 Omniglot, mini-ImageNet은 새로운 방법론들을 검증하기에 한계에 접근했으며 이 분야의 추가 진전을 위해서는 더 도전적이고 현실적인 벤치 마크가 필요

기존 벤치마크의 한계
 1) 동종의 task만 고려한다. 하지만 현실에서는 클래스 숫자나 샘플 숫자가 다양하며, class unblance가 많음
 2) 데이터셋 간 일반화만 측정한다. 그러나 완전히 새로운 분포(데이터셋)에 일반화할 수 있는 모델이 필요
 3) 에피소드를 구성할 때 클래스 간의 관계를 무시. 개와 의자의 거친 분류는 개 품종의 세분화된 분류와는 다른 어려움을 나타낼 수 있으며, 현재의 벤치 마크는 두 가지를 구별하지 않음

이를 개선하기 위해 훨씬 더 크고 다양한 데이터 분포의 여러 데이터셋을 구성  
ImageNet과 Omniglot 처럼 구조화 하며 현실적인 클래스 불균형을 도입  
각 작업의 클래스 수와 훈련 세트의 크기를 변화시켜 스펙트럼 전반에 걸친 모델의 견고성을 테스트

주요 contributions
 1) 트레이닝 및 테스트를 위한 보다 현실적이고 대규모 환경 제공
 2) 이에 대한 기존 모델들의 벤치마크 결과 취합
 3) 추가데이터, 다양한 학습 소스, pre-trained weighte, 메타러닝으로 인한 각 모델 별 장점 분석
 4) 새로운 메타러닝 모델 제안

## Background
#### Task Formulation
few-shot classification의 최종 목표는 N개의 클래스와 극소량의 레이블이 붙은 예제를 가진 새로운 학습 에피소드를 통해 해당 에피소드에서 다루지 않았던 example에 일반화 된 모델을 생성하는 것  
N개의 클래스와 클래스 별 k개의 샘플로 구성 된 에피소드 : N-way, k-shot 에피소드  

전체 클래스들의 집합 C를 Ctrain, Ctest의 서로소 집합으로 나눔
각 에피소드에서 Ctrain은 meta-training(support), meta-testing(query)에 활용하고 Ctest는 few-shot learning 성능 평가에 활용
Ctrain(support, query)를 통해 학습되는 모델을 meta-learner로 칭함

#### Non-episodic Approaches to Few-shot Classification
Ctrain에 대해 클래스당 하나의 output을 갖는 분류기를 한 번에 훈련 시킴
k-NN과 finetune이 이에 속함
여기서는 A CLOSER LOOK AT FEW-SHOT CLASSIFICATION의 Baseline++를 벤치마크

#### Meta-Learners for Few-shot Classification
Matching Networks (Vinyals et al., 2016), Relation Networks (Sung et al., 2018), PrototypicalNetworks (Snell et al., 2017), Model Agnostic Meta-Learning (MAML, Finn et al., 2017)
마지막 두 모델에서 영감을 얻은 새로운 meta-learner를 소개

##### Prototypical Networks
프로토타입 네트워크는 각 클래스에 대한 프로토타입을 구성한 다음 유클리드 거리 하에서 프로토타입이 가장 가까운 클래스로 각 query example을 분류
##### Matching Networks
query example을 support label과의 코사인가중 선형조합으로 labeling 함
##### Relation Networks
거리 계산 함수에 다층 퍼셉트론 적용  
다층 퍼셉트론은 같은 범주 또는 다른 범주의 서포트 데이터와 쿼리 데이터를 분류하는 법을 학습
#### MAML

#### Proto-MAML
이 연구에서 제안한 meta-learner
