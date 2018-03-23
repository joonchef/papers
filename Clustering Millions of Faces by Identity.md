# Clustering Millions of Faces by Identity

## 원문
https://arxiv.org/pdf/1604.00989.pdf

## 저자
* Charles Otto, Student Member, IEEE
* Dayong Wang, Member, IEEE
* Anil K. Jain, Fellow, IEEE

## Abstract
 이 연구에서는 다음과 같은 문제를 해결하려고합니다. 많은 수의 레이블이없는 얼굴 이미지가 주어지면, 이 데이터에있는 개별ID로 클러스터링합니다. 우리는 소셜 미디어에서 법 집행에 이르기까지 다양한 애플리케이션 시나리오에서 이와 관련된 문제를 고려합니다. 대규모 시나리오에서 컬렉션의 얼굴 수는 수천만 개에 달할 수 있지만 클러스터 수는 수천에서 수백만까지 다양하므로 런타임 복잡성과 클러스터링 평가면에서 어려움을 겪습니다. 효율적이고 효과적인 Rank-Order 클러스터링 알고리즘은 k-means 및 스펙트럼 클러스터링과 같은 다른 잘 알려진 알고리즘보다 나은 확장성 및 클러스터링 정확도를 얻기 위해 개발되었습니다. 최대 1억 2천 3백만개의 얼굴 이미지를 1천만개 이상의 클러스터에 클러스터링하고 외부 클러스터 품질 측정 값(알려진 얼굴 레이블)및 내부 클러스터 품질 측정 값(알 수 없는 얼굴 레이블)및 런타임과 관련하여 결과를 분석합니다. 우리의 알고리즘은 13,000 개의 얼굴로 구성된 LFW얼굴 데이터 세트와, 고려된 가장 큰 데이터 세트(LFW의 13K 이미지와 123M distractor 이미지)에서 각각 F-measure 0.87과 0.27을 달성합니다. 또한 비디오 프레임 클러스터링에 대한 예비 작업을 수행합니다 (벤치 마크 YouTube Faces 데이터 세트의 모든 프레임을 클러스터링 할 때 0.71 F-measure을 달성 함). 개별 클러스터를 순위 지정하고 수동 탐색을 위해 양질의 클러스터의 하위 집합을 자동으로 식별하는 데 사용할 수있는 클러스터 별 품질 측정 값이 개발되었습니다.

## 소개
이 작업에서는 다음과 같은 문제를 해결하려고합니다. 많은 수의 레이블이 없는 얼굴 이미지가 있으면 이 데이터에 있는 개별ID로 클러스터링
 합니다. 이러한 상황은 소셜 미디어에서 법 집행에 이르기까지 다양한 응용 프로그램 시나리오에서 발생합니다. 컬렉션의 얼굴 수는 수억 수천입니다. 종종 얼굴 이미지에 첨부 된 레이블이 누락 되었거나 노이즈가 포함되어 있습니다. 클러스터의 수 또는 알 수없는 ID 수는 수천에서 수억까지 다양하므로 런타임과 클러스터링 품질 측면에서 어려움이 있습니다.
Facebook은 소셜미디어를 고려할 때 하루 평균 3억 5천만개의 이미지가 업로드 되고 있다고 보고했으며 그 중 상당수는 사람들의 이미지라고 합리적으로 추측 할 수 있습니다. 소셜미디어에서 ID정보는 태깅을 통해 제공 될 수 있지만 일반적으로 이는 불완전하고 부정확 할 수 있습니다. 우리는 이 대량의 데이터를 구성하기 위한 하나의 가능한 접근방식으로 얼굴 이미지를 개별ID로 그룹화하는 것을 고려합니다.
법의학 조사에서 대규모 얼굴 수집을 수집하는 것도 새로운 문제입니다. 보스턴 마라톤 폭탄 테러는 대표적인 사례입니다. 보스턴 마라톤 폭탄 사건 수사는 시간에 민감했는데, 시급히 수만개의 이미지와 비디오를 분석해야했습니다. 대규모 미디어 컬렉션 조사를 필요로 하는 기타 일반적인 경우는 아동 학대 사례에서 가해자 및 희생자 식별, 소셜 미디어 컬렉션에서 어떤 개인이 어떤 그룹에 속하는지 식별(갱단 및 테러리스트 네트워크의 이미지와 같은), 하드드라이브에서 미디어컬렉션 생성(개인용 컴퓨터 또는 서버) 등이 있습니다.
소셜 미디어와 법의학 조사에서 우리는 데이터 집합에 존재하는 알려지지 않은 얼굴의 수가 많을 것으로 기대합니다. 이것은 런타임이 클러스터의 수와 관련이 있기 때문에 확장성 관점에서 도전적입니다. 또한 개인 별 이미지 수의 균형이 맞지 않을 것으로 예상되므로(어떤 사람들은 자주 나타나고 다른 사람들은 덜 나타날 수 있습니다), k-means와 같은 유사한 수의 클러스터를 생성하는 알고리즘에 비해 도전적입니다.
또한 포즈, 조명, 오클루전 등의 이미지 품질은 상대적으로 낮다고 가정 할 수 있습니다. 소셜미디어 이미지, 공개 이벤트 등에서 촬영 한 이미지는 일반적으로 얼굴분석에 가장 적합한 조건으로 캡처되지 않기 때문입니다. 제약없는 얼굴 인식에 대한 최근의 진보에 따라 우리는 최첨단 컨볼 루션 신경망 기반의 얼굴 표현을 사용하여 근본적인 얼굴 클러스터링 문제의 어려움을 완화하려고 시도합니다
 강력한 얼굴 표현을 사용하더라도 정확성은 확인 작업에 완벽하지 않습니다. Zhu는 비교하려는 얼굴 이미지들의 공통적인 가장 가까운 이웃을 기반으로 거리를 측정하는 Rank-Order 클러스터링 방법을 사용하여 개인 사진 모음을 클러스터링하는 데 성공했다고 보고했습니다.(직접적인 feature vector - feature vector 거리가 얼굴 인식 작업의 어려움에 따라 부정확 할 수 있기 때문에) 그러나 이미지 품질 문제까지 있기 때문에 대규모 클러스터링은 확장성 측면에서 본질적으로 어렵다. 우리는 확장 성을 높이기 위해 근사 이웃 노드 방법을 활용하고 실제 클러스터링 절차를 단순화하여 확장 성 및 클러스터링 정확도 향상시키는, Zhu의 Rank-order 클러스터링 알고리즘의 한 버전을 개발합니다. 우리는 LFW 데이터셋의 레이블이있는 얼굴들과 레이블이 지정되지 않은 123M 이미지들을 클러스터링하여 대규모 클러스터링 성능을 평가합니다.
또한 실제 크기가 큰 데이터 세트를 합리적으로 정확하게 클러스터링하더라도 여전히 많은 클러스터가 수동으로 조사 될 수 있다는 점을 고려하여 클러스터 단위 내부 품질 측정을 조사하여 수동 클러스터링을 위한 양호한 클러스터의 하위 집합을 식별합니다. 제한되지 않은 스틸 얼굴 이미지의 대규모 클러스터링 외에도 YouTube Faces 데이터베이스를 활용 한 비디오 프레임 클러스터링에 대한 사전 조사를 수행하여 수십만 개의 비디오 프레임을 클러스터링합니다.

## Background
### Face Clustering
탐색 데이터 분석 도구 인 클러스터링 문제는 패턴 인식, 통계 및 기계 학습 문헌에서 잘 연구되어 왔습니다. 특히 이미지 수와 클러스터 수가 매우 많은 경우 얼굴 이미지를 클러스터링하는 것이 어려운 문제입니다. 얼굴 이미지를 클러스터링 (및 분류)하는 데 중요한 고려 사항은 보편적인 얼굴 표현 또는 거리 메트릭이 없으므로 클러스터링 결과는 클러스터링 알고리즘의 선택뿐만 아니라 기본 얼굴 표현의 품질 및 metric에 의해 결정됩니다. 표 1은 얼굴 표현 및 클러스터링 알고리즘이 사용 된 얼굴 클러스터링에 대한 이전 작업을 얼굴 이미지 및 고용인 수에 따라 사용 된 가장 큰 데이터 세트 크기와 함께 나열합니다.
### Approximate Nearest Neighbor Methods
잘 알려진 클러스터링 알고리즘들의 공통적인 문제는 데이터셋에 있는 n개의 모든 샘플들에 대한 가장 가까운 이웃집합을 찾는것입니다. 단순하게 O(n^2)시간복잡도는 큰 n에 대해 문제가 됩니다. 이것은 k-NN 그래프 생성 문제의 인스턴스로 간주 될 수 있으며, 또는 n 개의 근사 인접 노드 탐색 집합으로 간주 될 수 있습니다. 이 두 경우 모두 근사 방법을 문헌에서 찾을 수 있습니다.
#### k-nn Graph Construction
전체 k-NN 그래프를 계산하기 위한 하나의 근사법은 Chen에 의해 알려졌습니다. 이 알고리즘은 Lanczos 이분법을 통해 특징 공간을 재귀 적으로 세분화 한 절차입니다. 우리는이 알고리즘의 병렬화 된 버전을 사용하는데,이 알고리즘은 각각의 재귀 적 하위 구분에서 분기되어 별도의 스레드에서 각각을 모두 처리합니다. 이 알고리즘은 일부 비교 집합을 건너 뜀으로써 brute-force 방법보다 향상된 런타임을 얻습니다. 따라서 런타임은 선택된 겹침 정도의 함수입니다
#### Randomized k-d Tree
k-NN 그래프 구조 외에도 전체 이웃 탐색 문제로 전체 데이터 세트에 대한 가장 가까운 이웃리스트를 구축하는 것이 고려 될 수 있으며 근사 이웃 탐색 방법을 사용하여 전체 런타임을 향상시킬 수 있습니다. 여러 NN알고리즘 중 전통적인 유형은 분할트리기반 방법입니다.
그들은 고전적인 k-d 트리 알고리즘을 따릅니다.이 알고리즘은 데이터를 분할하는 기능의 하위 집합을 선택하여 기능 공간을 세분하는 인덱스를 만듭니다. Randomized k-d 트리 알고리즘은 여러 무작위 k-d 트리 인덱스를 구축하여 효율성을 향상시킨 다음 해당 인덱스를 병렬로 검색합니다
### Clustering Evaluation
클러스터링 성능을 평가할 때 "올바른"클러스터링 (ID로 클러스터링)의 사전 정의를 사용하므로 우리는 알려진 신원 레이블에 상응하는 클러스터 측면에서 정확성을 평가할 수 있습니다. 클러스터링 품질을 평가하기 위한 외부 조치는 신원 레이블에 의존합니다. 우리는 pairwise precision / recall을 효율적으로 계산할 수 있기 때문에 사용할 것입니다. 실행 시간 또한 중요한 평가 기준입니다.
 쌍방향 정밀도는 데이터 집합 내의 모든 동일한 클러스터 쌍 수에 대해 동일한 클래스 (동일한 ID를 가짐) 인 (가능한 모든 쌍을 고려하여) 클러스터 내의 샘플 쌍의 비율로 정의됩니다. 페어 와이즈 리콜 (pairwise recall)은 데이터 집합의 동일 클래스 쌍의 총 수에 대해 동일한 클러스터에 배치 된 클래스 내의 샘플 쌍 (가능한 모든 쌍을 고려)의 비율로 정의됩니다. 이러한 측정은 두 가지 유형의 오류를 캡처합니다. 즉, 개별 클러스터가 높은 정밀도를 갖지만 낮은 회수율을 갖는 모든 샘플을 배치하는 클러스터링은 동일한 클러스터에 모든 샘플을 배치하는 클러스터링이 높은 리콜을 가지지 만 정밀도는 낮습니다. F-measure F = 2 × (P recision × Recall)/(P recision + Recall).
우리는 대규모 클러스터링 문제에서 볼 수 있듯이 평가에서 레이블이 지정되지 않은 데이터를 간단히 생략함으로써 가능한 한 범위 내에서 부분적으로 레이블 된 데이터를 처리하도록 이러한 방법을 확장합니다. 실험에서 웹에서 다운로드 한 레이블이 없는 수많은 얼굴과 레이블이있는 LFW를 혼합하므로 부분적으로 레이블링 된 데이터가 발생합니다.
 레이블이 없는 ID가 함께 그룹화 되는지 여부를 계산하지 않음으로써 수정 된 쌍 단위 호출을 정의합니다. 정확도를 위해 unlabeled-labeled쌍과 불일치를 고려하고 계산에서 unlabeled-unlabeled쌍을 생략합니다. 따라서 주어진 클러스터에서 가능한 모든 쌍을 고려하기보다는 합계에서 unlabeled-unlabeled 쌍을 생략합니다.

## PROPOSED FACE CLUSTERING APPROACH
### Face Representation
 제한되지 않은 상황에서 캡쳐된 얼굴 이미지들을 클러스터링해야 하기 때문에, 성공적인 연구결과가 있는 Deep CNN을 얼굴표현 방식으로 사용합니다. 많은 deep learning 접근법이 LFW 벤치 마크에 성공적으로 적용되었습니다. 그러나 대부분이 private 트레이닝 데이터셋을 활용합니다. 우리의 경우 D. Wang, C. Otto, and A. K. Jain, “Face search at scale: 80 million gallery,”에 정의된 아키텍쳐를 사용하고 CASIA-webface 데이터셋을 이용하여 직접 학습시킵니다. 입력 이미지가 주어지고, Kazemi and Sullivan regression tree 앙상블 방법으로 68개의 랜드마크를 찾아냅니다. 검출된 키포인트들을 기반으로 정규화가 수행되고 특히 얼굴 회전은 눈사이 각도를 사용해 보정되고 eye-line은 이미지 상단에서 이미지 height의 45%위치에 배치됩니다. mouth-line은 이미지 하단으로부터 25%지점에 배치됩니다. 모든 검출 된 점들의 중간 점은 x 차원에서 중심에 위치하며, 정렬 된 이미지는 110x110로 스케일링되고, 중앙 100x100 영역은 최종 정규화 된 이미지 입니다. 정규화 된 이미지는 K. Simonyan and A. Zisserman, “Very deep convolutional networks for large-scale image recognition,” 에서 소개 된 10개의 convolutional layer와 3X3필터들로 구성 된 very deep 아키텍쳐로 전달 됩니다. 아키텍쳐는 convolutional layer 쌍과 이어지는 max 풀링 레이어가 4번 반복 된 후, 2개의 convolutional layer와 하나의 average 풀링 레이어가 이어진다. 마지막 convolutional layer를 제외하고는 모두 ReLU 활성화 함수를 사용한다. 마지막 320차원 결과를 feature로 사용하고 softmax loss가 뒤에 붙는 fully connected layer로 입력 됩니다. 320차원의 입력만 클러스터링에 사용됩니다. 네트워크는 10533명의 404992개의 얼굴이미지 데이터셋을 minibatch stochastic gradient descent 방식으로 학습합니다. 모든 레이어의 weight decay는 0.0005이고 learning rate는 0.01부터 0.00001까지 감소시킵니다. 네트워크는 cuda-convnet2 library로 구현되었습니다.
### Clustering Method
