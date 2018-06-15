Abstract
1000가지 클래스로 구분되어있는 120만장의 고해상도 이미지 분류를 위해 Deep CNN을 학습시킴.
테스트 데이터기준 top-1 37.5%, top-5 17.0%의 에러율을 달성(기존 방법들보다 우수)
Deep CNN은 6천만 파라미터와 65만뉴런, 5개의 convolutional 레이어 - max-pooling 레이어 셋, 
최종 1000개의 softmax로 분류하는 총 3개의 fully-connected 레이어로 이루어짐
빠른 학습을 위해 non-saturating 뉴런과 convolutional 연산에 매우 효과적인 GPU구현을 사용
오버피팅을 방지하기 위해 fully-connected 레이어에 효과가 입증 된 Dropout을 적용
ILSVRC-2012 대회에서 top-5 에러율 15.3%를 달성하여 우승(2위 26.2%)

Architecture
ReLU가 tanh보다 학습속도면에서 낫다. 대규모 모델에서 대규모 데이터로 학습 할 때 학습속도는 성능에 큰 영향을 미친다.
GPU메모리가 부족해 network를 2개의 GPU로 분산시켰다. 요즘 GPU들은 분산병렬처리에 적합하게 설계되어 호스트 메모리를 거치지
않고도 서로 직접 메모리에 접근할 수 있음.
근본적으로 사용한 병렬화 방법은 각 GPU에 뉴런을 반씩 분배함. GPU간 커뮤니케이션은 certain layer(특정 layer란 뜻인듯)에서만 한다는 트릭 포함
Local Response Normalization을 통해 error율 1.4% 가량 더 낮출 수 있었음
 https://prateekvjoshi.com/2016/04/05/what-is-local-response-normalization-in-convolutional-neural-networks/
 http://neurowhai.tistory.com/134
통상적으로 pooling 시 2x2 윈도우 size와 2의 stride값을 사용하는데, 3x3 윈도우 size와 2의 stride를 사용해 overlapping을 발생시킴으로써
에러율을 약 0.4% 줄일 수 있었다
2, 4, 5번째 Conv layer는 같은 GPU에 있는 이전 Layer의 output만 input으로 함
Response-Normalization layer는 1, 2번째 Conv layer 뒤에 붙음
Max-pooling layer는 Response-Normalization layer뒤와 5번째 Conv layer 뒤에 붙음
ReLU는 모든 Conv layer와 fully-connected layer 뒤에 붙음

Reducing Overfitting
256x256 이미지에서 랜덤으로 224x224 이미지를 추출하여 horizontal reflection한 데이터를 학습(트레이닝 데이터셋 2048배 증가)
테스트시에는 4개의 코너와 중앙 224x224 이미지를 horizontal reflection한 10개의 patch의 예측결과를 평균함
RGB에 PCA를 수행하여 top-1 에러율을 1%이상 낮춤
1, 2번째 fully-connected layer에 dropout을 적용. 
학습 시 0.5 probability로 dropout, 테스트 시 모든 뉴런사용하는 대신 0.5 probability의 뉴런의 output에 0.5를 곱함

Details of learning
stochastic gradient descent를 사용하고, 128 batch size, 0.9 momentum, 0.0005 weight decay를 사용
모든 layer의 weight를 zero-mean Gaussian 분포(편차 0.01)로 초기화
2, 4, 5번째 Conv layer와 fully-connected layer의 bias를 1로 초기화(ReLU에 양수값을 입력으로 하여 학습 초기단계 가속화)
나머지 layer의 bias는 0으로 초기화
learning rate는 0.01로 시작하여 validation 에러율의 개선이 없을때 마다 0.1을 곱함(총 3번) 
약 90 cycle 학습(2 x gtx580 3GB GPU로 5~6일)

Result

Discussion
더 많은 layer를(더 Deep한 Networks )사용하면 더 좋은 성능을 달성 할 수 있을 것

