#Abstract
large-scale 이미지 인식에서 convolutional network의 깊이에 따른 효과를 조사하기 위한 작업
3x3 convolutional 필터들을 사용하여 기존 network들의 깊이를 16, 19 레이어로 늘려서 눈에띄는 성능향상을 보여줌

#ConvNet Configuration
##Architecture
training input : 224x224 rgb
preprocessing : rgb mean subtracting
convolution stride : 1(fixed)
max-pooling : 모든 conv layer뒤에 붙진 않으며 2x2 window size, 2 stride
##Configurations
표에 잘 나와있음

#Classification Framework
##Training
batch size : 256
momentum : 0.9
weight decay : 0.0005
dropout : 처음 2개의 fc layer뒤(ratio : 0.5)
learning-rate : 0.01로 시작해서 validation set의 정확도가 개선되지 않을때 0.1을 곱함(총 3회)
370000 iteration, 74 epoch 학습
많은 parameter와 깊은 depth에도 불구하고 더 적은 epoch
(깊어진 깊이와 작은 필터 덕분에 implicit regularization이 겹쳐짐, 특정 layer pre-initialization)
랜덤 initialization으로 학습될 정도로 얕은 configuration A로 시작
더 깊은 아키텍쳐의 처음 4개의 conv 레이어와 3개의 fc레이어를 A net의 값들로 초기화(나머지 레이어는 랜덤)
랜덤 초기화에는 zero mean, 0.01 분산 사용
bias는 0으로 초기화
image size : crop은 224x224로 고정, 원본 이미지의 가장 작은 변의 길이를 S
crop image는 작은 object나 object의 일부분을 포함할 수 있음
1) S = 384, 256
2) S = random (Smin = 256, Smax = 512)
##Testing
image size : 원본 이미지의 가장 작은 변의 길이를 Q (S와 같을 필요는 없음)
horizontal-flip, original의 softmax 평균을 final score로 사용

##Classification Experiments
#Single Scale Evaluation
S = Q (S가 fixed일때)
S = (256 + 512) / 2 = 384 (S가 random[256:512]일때) => E net : 25.5%, 8.0%
#Multi Scale Evaluation
S = 256, Q = 224, 256, 288
S = 384, Q = 352, 384, 416
S = [256, 512], Q = 256, 384, 512 => D, E net : 24.8%, 7.5%
#Multi-crop Evaluation

