# Stacked Generative Adversarial Networks

## 원문
http://openaccess.thecvf.com/content_cvpr_2017/papers/Huang_Stacked_Generative_Adversarial_CVPR_2017_paper.pdf

## 저자
* Xun Huang, Department of Computer Science, Cornell University 
* Yixuan Li, School of Electrical and Computer Engineering, Cornell University
* Omid Poursaeed, School of Electrical and Computer Engineering, Cornell University
* John Hopcroft, Department of Computer Science, Cornell University
* Serge Belongie Department of Computer Science, Cornell University, Cornell Tech

## Abstract
본 논문에서는 SGAN (Stacked Generative Adversarial Networks)이라는 새로운 생성 모델을 제안한다.이 모델은 bottom-up discriminative 네트워크의 계층 적 표현을 뒤집을 수 있도록 훈련되어있다. 우리 모델은 GAN의 하향식 스택으로 구성되어 있으며, 각각 상위 레벨 표현에 따라 하위 레벨 표현을 생성하는 방법을 학습한다. 표현 식별기는 생성기의 표현 다양체가 강력한 차별화 표현을 활용하여 생성 모델을 유도함으로써 상향식 차별 네트워크의 표현 다양체와 일치하도록 유도하기 위해 각 기능 계층 구조에 도입됩니다. 또한 위의 계층에서 조건부 정보를 사용하도록 권장하는 조건부 손실과 발전기 출력의 조건부 엔트로피에 대한 변형 하한을 최대화하는 새로운 엔트로피 손실을 소개합니다. 우리는 먼저 각 스택을 독립적으로 트레이닝 한 다음 전체 모델을 엔드 투 엔드로 교육합니다. 단일 노이즈 벡터를 사용하여 모든 변형을 나타내는 원래 GAN과 달리 SGAN은 변형을 여러 수준으로 분해하고 하향식 생성 프로세스에서 불확실성을 점차 해결합니다. 시각적 검사, 초기 점수 및 시각적 튜링 테스트를 기반으로 SGAN이 스태킹없이 GAN보다 훨씬 높은 품질의 이미지를 생성 할 수 있음을 보여줍니다

## Introduction

