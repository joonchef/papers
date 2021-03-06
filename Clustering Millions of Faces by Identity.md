Clustering Millions of Faces by Identity
========================================
# 원문
https://arxiv.org/pdf/1604.00989.pdf

# 저자
* Charles Otto, Student Member, IEEE
* Dayong Wang, Member, IEEE
* Anil K. Jain, Fellow, IEEE

# Abstract
 이 연구에서는 다음과 같은 문제를 해결하려고합니다. 많은 수의 레이블이없는 얼굴 이미지가 주어지면, 이 데이터에있는 개별ID로 클러스터링합니다. 우리는 소셜 미디어에서 법 집행에 이르기까지 다양한 애플리케이션 시나리오에서 이와 관련된 문제를 고려합니다. 대규모 시나리오에서 컬렉션의 얼굴 수는 수천만 개에 달할 수 있지만 클러스터 수는 수천에서 수백만까지 다양하므로 런타임 복잡성과 클러스터링 평가면에서 어려움을 겪습니다. 효율적이고 효과적인 Rank-Order 클러스터링 알고리즘은 k-means 및 스펙트럼 클러스터링과 같은 다른 잘 알려진 알고리즘보다 나은 확장성 및 클러스터링 정확도를 얻기 위해 개발되었습니다. 최대 1억 2천 3백만개의 얼굴 이미지를 1천만개 이상의 클러스터에 클러스터링하고 외부 클러스터 품질 측정 값(알려진 얼굴 레이블)및 내부 클러스터 품질 측정 값(알 수 없는 얼굴 레이블)및 런타임과 관련하여 결과를 분석합니다. 우리의 알고리즘은 13,000 개의 얼굴로 구성된 LFW얼굴 데이터 세트와, 고려된 가장 큰 데이터 세트(LFW의 13K 이미지와 123M distractor 이미지)에서 각각 F-measure 0.87과 0.27을 달성합니다. 또한 비디오 프레임 클러스터링에 대한 예비 작업을 수행합니다 (벤치 마크 YouTube Faces 데이터 세트의 모든 프레임을 클러스터링 할 때 0.71 F-measure을 달성 함). 개별 클러스터를 순위 지정하고 수동 탐색을 위해 양질의 클러스터의 하위 집합을 자동으로 식별하는 데 사용할 수있는 클러스터 별 품질 측정 값이 개발되었습니다.

# 소개
이 작업에서는 다음과 같은 문제를 해결하려고합니다. 많은 수의 레이블이 없는 얼굴 이미지가 있으면 이 데이터에 있는 개별ID로 클러스터링
 합니다. 이러한 상황은 소셜 미디어에서 법 집행에 이르기까지 다양한 응용 프로그램 시나리오에서 발생합니다. 컬렉션의 얼굴 수는 수억 수천입니다. 종종 얼굴 이미지에 첨부 된 레이블이 누락 되었거나 노이즈가 포함되어 있습니다. 클러스터의 수 또는 알 수없는 ID 수는 수천에서 수억까지 다양하므로 런타임과 클러스터링 품질 측면에서 어려움이 있습니다.
Facebook은 소셜미디어를 고려할 때 하루 평균 3억 5천만개의 이미지가 업로드 되고 있다고 보고했으며 그 중 상당수는 사람들의 이미지라고 합리적으로 추측 할 수 있습니다. 소셜미디어에서 ID정보는 태깅을 통해 제공 될 수 있지만 일반적으로 이는 불완전하고 부정확 할 수 있습니다. 우리는 이 대량의 데이터를 구성하기 위한 하나의 가능한 접근방식으로 얼굴 이미지를 개별ID로 그룹화하는 것을 고려합니다.
법의학 조사에서 대규모 얼굴 수집을 수집하는 것도 새로운 문제입니다. 보스턴 마라톤 폭탄 테러는 대표적인 사례입니다. 보스턴 마라톤 폭탄 사건 수사는 시간에 민감했는데, 시급히 수만개의 이미지와 비디오를 분석해야했습니다. 대규모 미디어 컬렉션 조사를 필요로 하는 기타 일반적인 경우는 아동 학대 사례에서 가해자 및 희생자 식별, 소셜 미디어 컬렉션에서 어떤 개인이 어떤 그룹에 속하는지 식별(갱단 및 테러리스트 네트워크의 이미지와 같은), 하드드라이브에서 미디어컬렉션 생성(개인용 컴퓨터 또는 서버) 등이 있습니다.
소셜 미디어와 법의학 조사에서 우리는 데이터 집합에 존재하는 알려지지 않은 얼굴의 수가 많을 것으로 기대합니다. 이것은 런타임이 클러스터의 수와 관련이 있기 때문에 확장성 관점에서 도전적입니다. 또한 개인 별 이미지 수의 균형이 맞지 않을 것으로 예상되므로(어떤 사람들은 자주 나타나고 다른 사람들은 덜 나타날 수 있습니다), k-means와 같은 유사한 수의 클러스터를 생성하는 알고리즘에 비해 도전적입니다.
또한 포즈, 조명, 오클루전 등의 이미지 품질은 상대적으로 낮다고 가정 할 수 있습니다. 소셜미디어 이미지, 공개 이벤트 등에서 촬영 한 이미지는 일반적으로 얼굴분석에 가장 적합한 조건으로 캡처되지 않기 때문입니다. 제약없는 얼굴 인식에 대한 최근의 진보에 따라 우리는 최첨단 컨볼 루션 신경망 기반의 얼굴 표현을 사용하여 근본적인 얼굴 클러스터링 문제의 어려움을 완화하려고 시도합니다
 강력한 얼굴 표현을 사용하더라도 정확성은 확인 작업에 완벽하지 않습니다. Zhu는 비교하려는 얼굴 이미지들의 공통적인 가장 가까운 이웃을 기반으로 거리를 측정하는 Rank-Order 클러스터링 방법을 사용하여 개인 사진 모음을 클러스터링하는 데 성공했다고 보고했습니다.(직접적인 feature vector - feature vector 거리가 얼굴 인식 작업의 어려움에 따라 부정확 할 수 있기 때문에) 그러나 이미지 품질 문제까지 있기 때문에 대규모 클러스터링은 확장성 측면에서 본질적으로 어렵다. 우리는 확장 성을 높이기 위해 근사 이웃 노드 방법을 활용하고 실제 클러스터링 절차를 단순화하여 확장 성 및 클러스터링 정확도 향상시키는, Zhu의 Rank-order 클러스터링 알고리즘의 한 버전을 개발합니다. 우리는 LFW 데이터셋의 레이블이있는 얼굴들과 레이블이 지정되지 않은 123M 이미지들을 클러스터링하여 대규모 클러스터링 성능을 평가합니다.
또한 실제 크기가 큰 데이터 세트를 합리적으로 정확하게 클러스터링하더라도 여전히 많은 클러스터가 수동으로 조사 될 수 있다는 점을 고려하여 클러스터 단위 내부 품질 측정을 조사하여 수동 클러스터링을 위한 양호한 클러스터의 하위 집합을 식별합니다. 제한되지 않은 스틸 얼굴 이미지의 대규모 클러스터링 외에도 YouTube Faces 데이터베이스를 활용 한 비디오 프레임 클러스터링에 대한 사전 조사를 수행하여 수십만 개의 비디오 프레임을 클러스터링합니다.

# Background
## Face Clustering
탐색 데이터 분석 도구 인 클러스터링 문제는 패턴 인식, 통계 및 기계 학습 문헌에서 잘 연구되어 왔습니다. 특히 이미지 수와 클러스터 수가 매우 많은 경우 얼굴 이미지를 클러스터링하는 것이 어려운 문제입니다. 얼굴 이미지를 클러스터링 (및 분류)하는 데 중요한 고려 사항은 보편적인 얼굴 표현 또는 거리 메트릭이 없으므로 클러스터링 결과는 클러스터링 알고리즘의 선택뿐만 아니라 기본 얼굴 표현의 품질 및 metric에 의해 결정됩니다. 표 1은 얼굴 표현 및 클러스터링 알고리즘이 사용 된 얼굴 클러스터링에 대한 이전 작업을 얼굴 이미지 및 고용인 수에 따라 사용 된 가장 큰 데이터 세트 크기와 함께 나열합니다.
## Approximate Nearest Neighbor Methods
잘 알려진 클러스터링 알고리즘들의 공통적인 문제는 데이터셋에 있는 n개의 모든 샘플들에 대한 가장 가까운 이웃집합을 찾는것입니다. 단순하게 O(n^2)시간복잡도는 큰 n에 대해 문제가 됩니다. 이것은 k-NN 그래프 생성 문제의 인스턴스로 간주 될 수 있으며, 또는 n 개의 근사 인접 노드 탐색 집합으로 간주 될 수 있습니다. 이 두 경우 모두 근사 방법을 문헌에서 찾을 수 있습니다.
### k-nn Graph Construction
전체 k-NN 그래프를 계산하기 위한 하나의 근사법은 Chen에 의해 알려졌습니다. 이 알고리즘은 Lanczos 이분법을 통해 특징 공간을 재귀 적으로 세분화 한 절차입니다. 우리는이 알고리즘의 병렬화 된 버전을 사용하는데,이 알고리즘은 각각의 재귀 적 하위 구분에서 분기되어 별도의 스레드에서 각각을 모두 처리합니다. 이 알고리즘은 일부 비교 집합을 건너 뜀으로써 brute-force 방법보다 향상된 런타임을 얻습니다. 따라서 런타임은 선택된 겹침 정도의 함수입니다
### Randomized k-d Tree
k-NN 그래프 구조 외에도 전체 이웃 탐색 문제로 전체 데이터 세트에 대한 가장 가까운 이웃리스트를 구축하는 것이 고려 될 수 있으며 근사 이웃 탐색 방법을 사용하여 전체 런타임을 향상시킬 수 있습니다. 여러 NN알고리즘 중 전통적인 유형은 분할트리기반 방법입니다.
그들은 고전적인 k-d 트리 알고리즘을 따릅니다.이 알고리즘은 데이터를 분할하는 기능의 하위 집합을 선택하여 기능 공간을 세분하는 인덱스를 만듭니다. Randomized k-d 트리 알고리즘은 여러 무작위 k-d 트리 인덱스를 구축하여 효율성을 향상시킨 다음 해당 인덱스를 병렬로 검색합니다
## Clustering Evaluation
클러스터링 성능을 평가할 때 "올바른"클러스터링 (ID로 클러스터링)의 사전 정의를 사용하므로 우리는 알려진 신원 레이블에 상응하는 클러스터 측면에서 정확성을 평가할 수 있습니다. 클러스터링 품질을 평가하기 위한 외부 조치는 신원 레이블에 의존합니다. 우리는 pairwise precision / recall을 효율적으로 계산할 수 있기 때문에 사용할 것입니다. 실행 시간 또한 중요한 평가 기준입니다.
 쌍방향 정밀도는 데이터 집합 내의 모든 동일한 클러스터 쌍 수에 대해 동일한 클래스 (동일한 ID를 가짐) 인 (가능한 모든 쌍을 고려하여) 클러스터 내의 샘플 쌍의 비율로 정의됩니다. 페어 와이즈 리콜 (pairwise recall)은 데이터 집합의 동일 클래스 쌍의 총 수에 대해 동일한 클러스터에 배치 된 클래스 내의 샘플 쌍 (가능한 모든 쌍을 고려)의 비율로 정의됩니다. 이러한 측정은 두 가지 유형의 오류를 캡처합니다. 즉, 개별 클러스터가 높은 정밀도를 갖지만 낮은 회수율을 갖는 모든 샘플을 배치하는 클러스터링은 동일한 클러스터에 모든 샘플을 배치하는 클러스터링이 높은 리콜을 가지지 만 정밀도는 낮습니다. F-measure F = 2 × (P recision × Recall)/(P recision + Recall).
우리는 대규모 클러스터링 문제에서 볼 수 있듯이 평가에서 레이블이 지정되지 않은 데이터를 간단히 생략함으로써 가능한 한 범위 내에서 부분적으로 레이블 된 데이터를 처리하도록 이러한 방법을 확장합니다. 실험에서 웹에서 다운로드 한 레이블이 없는 수많은 얼굴과 레이블이있는 LFW를 혼합하므로 부분적으로 레이블링 된 데이터가 발생합니다.
 레이블이 없는 ID가 함께 그룹화 되는지 여부를 계산하지 않음으로써 수정 된 쌍 단위 호출을 정의합니다. 정확도를 위해 unlabeled-labeled쌍과 불일치를 고려하고 계산에서 unlabeled-unlabeled쌍을 생략합니다. 따라서 주어진 클러스터에서 가능한 모든 쌍을 고려하기보다는 합계에서 unlabeled-unlabeled 쌍을 생략합니다.

# PROPOSED FACE CLUSTERING APPROACH
## Face Representation
 제한되지 않은 상황에서 캡쳐된 얼굴 이미지들을 클러스터링해야 하기 때문에, 성공적인 연구결과가 있는 Deep CNN을 얼굴표현 방식으로 사용합니다. 많은 deep learning 접근법이 LFW 벤치 마크에 성공적으로 적용되었습니다. 그러나 대부분이 private 트레이닝 데이터셋을 활용합니다. 우리의 경우 D. Wang, C. Otto, and A. K. Jain, “Face search at scale: 80 million gallery,”에 정의된 아키텍쳐를 사용하고 CASIA-webface 데이터셋을 이용하여 직접 학습시킵니다. 입력 이미지가 주어지고, Kazemi and Sullivan regression tree 앙상블 방법으로 68개의 랜드마크를 찾아냅니다. 검출된 키포인트들을 기반으로 정규화가 수행되고 특히 얼굴 회전은 눈사이 각도를 사용해 보정되고 eye-line은 이미지 상단에서 이미지 height의 45%위치에 배치됩니다. mouth-line은 이미지 하단으로부터 25%지점에 배치됩니다. 모든 검출 된 점들의 중간 점은 x 차원에서 중심에 위치하며, 정렬 된 이미지는 110x110로 스케일링되고, 중앙 100x100 영역은 최종 정규화 된 이미지 입니다. 정규화 된 이미지는 K. Simonyan and A. Zisserman, “Very deep convolutional networks for large-scale image recognition,” 에서 소개 된 10개의 convolutional layer와 3X3필터들로 구성 된 very deep 아키텍쳐로 전달 됩니다. 아키텍쳐는 convolutional layer 쌍과 이어지는 max 풀링 레이어가 4번 반복 된 후, 2개의 convolutional layer와 하나의 average 풀링 레이어가 이어진다. 마지막 convolutional layer를 제외하고는 모두 ReLU 활성화 함수를 사용한다. 마지막 320차원 결과를 feature로 사용하고 softmax loss가 뒤에 붙는 fully connected layer로 입력 됩니다. 320차원의 입력만 클러스터링에 사용됩니다. 네트워크는 10533명의 404992개의 얼굴이미지 데이터셋을 minibatch stochastic gradient descent 방식으로 학습합니다. 모든 레이어의 weight decay는 0.0005이고 learning rate는 0.01부터 0.00001까지 감소시킵니다. 네트워크는 cuda-convnet2 library로 구현되었습니다.
## Clustering Method
많은 수의 클러스터링 방법들이 제곱 오차, 혼합 모델, 가장 가까운 이웃 및 그래프 이론적 접근법에 기반한 문헌에서 제안되었다. "An efficient approach for clustering face images"에서 다룬 얼굴 클러스터링을 위한 접근법에 기초하여, 우리는 Zhu 등이 제안한 Rank-Order 클러스터링 알고리즘의 근사 버전을 이용한다. 원래의 알고리즘을 자세하게 제시 한 다음 우리의 수정 된 버전을 제시한다.
### Rank-Order Clustering
Zhu 등이 제안한 Rank-Order 클러스터링 알고리즘은 가장 가까운 이웃 기반 거리 측정을 사용하는 집적 계층 적 클러스터링의 한 형태인 Gowda와 Krishna 방법과 유사하다. 어떤 거리 메트릭 주어졌을 때 응집 계층적 클러스터링의 전체 절차는 모든 샘플을 개별 클러스터로 초기화 한 다음 가장 가까운 두 클러스터를 반복적으로 병합하는 것입니다. 이를 위해서는 클러스터 간 거리 측정 기준을 정의해야합니다. 이 알고리즘에서 두 클러스터 간의 거리는 클러스터 내  임의의 두 샘플 간의 최소 거리로 간주됩니다.
Rank-Order 클러스터링에서 사용되는 첫번째 거리 메트릭은 다음 식으로부터 주어진다.
 d(a, b) = sigma(i=1, Oa(b)) Ob(fa(i))       식(1)
여기서 fa(i)는 a의 이웃 리스트에 있는 i번 째 얼굴이고, Ob(fa(i))는 b의 이웃 리스트에 있는 얼굴 fa(i)의 rank를 나타낸다.
이 비대칭 거리 함수는 다음과 같이 a와 b 사이의 대칭 거리를 정의하는 데 사용된다.
D(a, b) = (d(a, b) + d(b, a)) / min(Oa(b), Ob(a))
대칭 Rank-Order 거리 함수는 두 얼굴이 서로 가까이 있으면 (얼굴 a가 얼굴 b의 이웃 목록에서 높은 순위이고, 얼굴 b가 얼굴 a의 이웃 목록에서 높은 순위에있을 때) 낮은 값을 반환하며 이웃을 공통으로한다 (높은 순위 얼굴 b의 이웃들은 얼굴 a의 이웃리스트에서도 높은 순위를 가진다) 거리 계산이 끝나면 모든 얼굴 이미지를 자체 클러스터로 초기화 한 다음 각 클러스터 간의 대칭 거리를 계산하고 임계 값 이하의 거리에있는 모든 클러스터를 병합하여 클러스터링을 수행한다. 그런 다음 새로 병합 된 클러스터에 대한 가장 가까운 인접 목록을 병합하고 나머지 클러스터 간의 거리를 더 이상 병합 할 수 없을 때까지 반복적으로 계산한다. 이 경우 원하는 클러스터 수 C를 지정하는 대신 거리 임계 값이 지정된다. 그것은 클러스터되는 특정 데이터 세트에 대한 특정 클러스터 수를 결정하는 임계 값이며, 유효 임계 값은 경험적으로 결정된다. 우리는 이 알고리즘의 자체 구현을 사용한다.
실행 시간 측면에서 각 샘플에 대한 가장 가까운 이웃리스트를 계산하는 것의 시간복잡도는 O (n^2)이다. 또한 여기에서 사용 된 실제 클러스터링 단계는 반복적인 비용으로 반복 당 비용이 클러스터의 현재 수에 비례하므로 (n에서 시작하고 반복을 통해 감소하는 클러스터의 수와 함께) 가장 가까운 이웃 계산과 클러스터링 단계 자체는 데이터 집합 크기가 커짐에 따라 비용이 많이 든다.
### Proposed Approximate Rank-Order Clustering
Rank-Order 클러스터링 방법은 데이터 집합의 모든 샘플에 대해 가장 가까운 이웃 목록을 계산(O(n^2))해야한다는 점에서 명백한 확장성 문제가 있다. 가장 가까운 이웃을 계산하기위한 다양한 근사화 방법이 존재하지만, 일반적으로 데이터 세트를 철저히 랭킹하는 것보다는 상위 k 개의 가장 가까운 이웃의 짧은 목록만을 효율적으로 계산할 수 있다. 우리는 랜덤 화 된 k-d 트리 알고리즘("Scalable nearest neighbor algorithms for high
dimensional data")의 FLANN 라이브러리 구현을 사용하여 가장 가까운 이웃의 짧은 목록을 계산한다.
가장 가까운 이웃 계산을 위한 근사 방법을 적용하면 원래의 Rank-Order 클러스터링 알고리즘을 약간 수정해야한다. 특히 합계 방정식 식(1)에서 모든 이웃을 고려하기보다는 클러스터 생성이 지역 주변에 의존한다는 가정하에 최대 k개의 이웃을 합산한다.
더욱이 우리는 짧은 k-list의리스트 만 고려한다면 짧은리스트의 특정 예제의 존재 여부가 샘플의 수치 적 순위보다 더 중요 할 수 있음을 알 수있다. 이와 같이, 랭크보다는 공유 된 가장 가까운 이웃의 존재 / 부존재를 직접 합산하는 것에 기초한 거리 측정을 고려하여 Ib(x, k)는 얼굴 x가 얼굴 b의 k번째 안에 드는 가까운 이웃이면 0, 아니면 1을 반환하는 지시함수라고 할 때 다음과 같은 거리 함수를 얻을 수 있다.
dm(a, b) = sigma(i=1, min(Oa(b), k)) Ib(Ob(fa(i)), k)
실제적으로, 이 변형은 원래 공식 에서처럼 순위를 직접 합산하는 것과 비교할 때 클러스터링 정확도가 향상된다는 것을 알 수 있다.
효과적으로, 이 거리 함수는 가장 가까운 이웃리스트의 상단에 공통 이웃의 존재 또는 부재 (순위 200 위 이내)가 중요하다는 것을 의미하는 반면, 그것들의 순위 자체는 중요하지 않음을 의미한다.
원래의 알고리즘에서 사용 된 표준화 절차(비교되는 다른 샘플의 순위까지 ​​합산하고 min(Oa(b), Ob(a))로 나눈 것)는 여전히 ​​효과적이며, 수정 버전의 경우 더 정확한 클러스터링 결과를 제공한다. 수정 된 거리측정 함수는 다음과 같이 정의된다.
Dm(a, b) = (dm(a, b) + dm(b, a)) / min(Oa(b), Ob(a)    식(4)
또한 클러스터링 단계 자체의 런타임을 향상시키기 위해 가장 가까운 이웃을 공유하는 샘플 간의 거리 만 계산하고 개별 얼굴을 클러스터로 한 번만 병합한다.
이것은 기존의 알고리즘이 C^2번의 클러스터링을 수행하는 반면 우리는 단 한번의 클러스터링을 수행하는 것을 뜻한다. 또한 모든 가능한 페어의 부분집합(각 샘플 별 200개까지의 근접한 이웃만 고려하므로)에 대해서만 머지를 위한 체크를 하는것은 최종 클러스터링 비용이 O(n)임을 의미한다. (가까운 이웃목록이 이미 계산되어있다고 가정할때)	
최종 클러스터링 절차는 다음과 같다:
1) 데이터셋의 모든 얼굴에 대한 deep feature 추출
2) 데이터셋의 각 얼굴에 대해 k번째 근접 이웃들까지 계산
3) 식(4)에 따라 각 얼굴과 그것의 k번째 까지 가장 가까운 이웃리스트 간의 pairwise distance를 계산합니다.
4) 일시적으로 임계값 이하의 모든 얼굴들의 쌍을 머지한다
클러스터의 수 C를 결정하기 위해 주어진 데이터셋에 대해 임계 값을 선택하는것은 데이터 클러스터링의 오래 된 어려운 이슈이다. 실제 응용 프로그램에서는 실제 클러스터 수를 선험적으로 알 수 없으므로 실제 클러스터 수를 결정하는 강력한 절차가 없기때문에, 몇 가지 유효한 C 값으로 알고리즘을 평가하고 우리의 실험에서 얻은 최상의 결과를 리포트 한다.
## Per-Cluster Quailty Evaluation
우리의 전반적인 목표는 레이블이 없는 얼굴 이미지의 매우 큰 컬렉션에 대한 조사를 용이하게하는 것이다. 우리는 첫 번째 접근법으로 identity에 의한 얼굴 이미지 클러스터링을 제안했지만 매우 큰 데이터 세트의 경우 identity에 의한 클러스터링 조차도 수동 탐사를 위해 너무 많은 클러스터를 생성할 수 있다. 	우리는 내부 클러스터 유효성 측정을 사용하여 수동 조사에 적합한 개별 클러스터의 하위 집합을 식별함으로써 이 문제를 해결하려고 한다.
데이터셋이 완전히 레이블링되지 않은 실제 응용 프로그램에서는 외부 레이블에 따라 클러스터링을 평가할 수 없다. 그러나 레이블을 사용하지 않고 클러스터 품질 측정을 시도하는 내부 클러스터 품질 측정 방법에 관한 문헌("Algorithms for Clustering Data")이 있다. 이러한 측정 값은 일반적으로 조밀(클러스터 구성원이 쌍 방향 유사성으로 그룹화되는 정도) 또는 격리(클러스터 간 유사성으로 서로 다른 클러스터가 얼마나 잘 분리되는지)의 척도로 이해할 수 있다. 또한 우리는 데이터셋에 대한 클러스터링의 전반적인 품질 평가와 부분 클러스터링의 개별클러스터들의 품질 평가를 구분할 수 있다. 우리는 개별 클러스터 순위를 매기는 수단으로 클러스터 별 품질 측정을 사용할 것이다.
매우 큰 데이터셋을 다룰 때 기본적인 관심사는 런타임이다. 일반적으로 데이터셋의 모든 샘플 간의 거리를 계산하는 것은 불가능하며 데이터셋에 존재하는 클러스터와 데이터셋이 모두 큰 경우 모든 클러스터 간의 거리를 계산할 수 없다. 이 경우 k-NN 그래프를 사전 계산하여 그래프 기반 품질 측정을 고려하고 계산 된 그래프를 사용하여 계산상의 문제를 완화하는 것이 자연스럽다.
커버리지 (Coverage)는 그래프의 전체 에지 집합에서 나타나는 클러스터 내부 에지의 비율로 정의된다.("Experiments on graph clustering algorithms") 우리는 이것을 클러스터별 품질 측정에 활용하기 위해 수정하여 현재 클러스터의 노드에서 아웃 바운드 된 에지 중 클러스터의 다른 노드에 연결되는 에지 비율을 per-cluster coverage로 정의한다. 모듈화 품질은 클러스터 간 연결성 척도 (그 노드들의 완전한 그래프에서 가능한 에지들 중 클러스터 내의 노드들 사이에 존재하는 에지들의 비율)와 클러스터 내 연결성 측정치 (전체 그래프에서 각 클러스터 쌍 사이의 가능한 에지에서 나오는 교차 클러스터 에지의 평균 비율)의 차이로 정의된다.
이러한 그래프 기반 측정은 특정 꼭지점 사이의 엣지의 유무만으로 공식화 된다. 그러나 전체 LFW 데이터셋에서 생성 된 non-singleton 클러스터에 대해 원래의 320 차원 기능 공간을 2 차원 t-SNE "Visualizing data using t-sne" 임베딩 한 그림 5를 보면 몇 가지 간단한 거리 기반 측정을 볼 수 있다. 이 시각화에서는 동일한 클러스터에 배치 된 모든 이미지 사이에 선이 그려진다. 한 가지 분명한 것은 일부 클러스터 할당 오류가 2차원 사상에서 큰 거리를 차지하며 원래의 feature 공간에서도 이러한 오류가 큰 거리에서 발생 할 것임을 알 수 있다. 따라서, 우리는 샘플에서 NN 리스트에 있는 같은 클러스터 내의 다른 샘플까지의 평균 거리(average intra-cluster distance), 그리고 샘플의 NN리스트에 포함되는 다른 클러스터의 샘플까지의 평균 거리 (average inter-cluster distance)를 주로하여 knn 그래프에 표시된 엣지들 간의 거리에 기반한 간단한 조밀도 및 격리도 측정을 고려할 것이다.

# Datasets
우리의 클러스터링 실험은 여러 가지 제약받지 않은 얼굴 데이터셋을 사용하는데, 클러스터 네트워크 학습을 위한 CASIA-webface, 클러스터링 평가를위한 Labeled Face in the Wild (LFW)및 YouTubeFaces (YTF) 데이터셋을 사용한다. 추가로 대규모 클러스터링 평가를 위해 123백만개의 레이블이없는 웹 얼굴 이미지 모음이 보강된다. 각 데이터셋의 얼굴 이미지 예제는 그림 6에 나와있다.
* LFW : 5,749 명의 13,233 개의 얼굴 이미지를 포함한다. 5,749명 중 4,069명은 얼굴 이미지가 하나 뿐이다. 데이터셋은 유명인과 공인인의 이미지를 검색하여 만들어졌고, 자동으로 감지 할 수있는 얼굴이 있는 이미지 만 유지된다.
* YTF : LFW와 비슷한 YouTube Faces (YTF) 데이터셋은 인터넷에서 수집 한 유명인 및 공인 비디오의 비디오로 구성된다. 이 데이터셋에는 3425개의 비디오의 621126 개의 개별 프레임으로 구성된 1595명의 사람이 포함된다. 얼굴이 감지 될 수있는 모든 비디오 프레임에 대해 인물에 대한 레이블이 제공된다. 실험에서 각 비디오의 주요 대상과 주어진 프레임에 있을 수 있는 레이블이 없는 개인간에 혼동을 피하기 위해 사전에 크롭한 프레임을 사용한다.
* Webfaces : 대규모 데이터셋에서 클러스터링 방법을 평가하기 위해 협력 연구 그룹은 크롤러를 사용하여 총 123,654,141개의 웹 이미지를 크롤링 했다. LFW와 유사하게 이 이미지들은 자동 얼굴 검출기, 특히 DLIB 얼굴 검출기로 감지 할 수있는 얼굴을 포함하도록 필터링 되었다.
* CASIA-webface : CASIA-webface 데이터셋에는 10575명(주로 유명 인사)의 494414 개의 이미지가 포함되어 있다. 그러나 우리는 일부 이미지에서 얼굴을 찾을 수 없어, 10533명의 404992 개의 얼굴 이미지를 사용하여 네트워크를 학습하였다.

# Experiments
이 섹션에서는 대규모 얼굴 클러스터링에 대한 전반적인 평가를 여러 단계로 설명한다. 먼저, 작은 데이터 세트에서 다양한 클러스터링 알고리즘을 평가하고, 사용 된 가장 가까운 근사치를 평가 한 다음 대규모 얼굴 클러스터링 실험을 수행하고, 마지막으로 비디오 클러스터링에 대한 예비 작업을 제시한다.
## Clustering Algorithm Evaluation
대규모 데이터셋의 성능을 조사하기 전에 ID별로 전체 LFW 데이터셋을 클러스터링 해보자. 한 가지 이슈는 LFW에서 인물 당 이미지 분포가 상당히 불균형하다는 것이다 (대부분의 인물들은 한장의 사진만 존재하는데, 데이터셋의 모든 이미지 중 약 1/3을 차지한다). 실제로 대규모 클러스터링의 적용 영역에 대해 더 균형 잡힌 클러스터를 사용하여 LFW의 하위 집합을 구성 할 수는 있지만 피사체 당 이미지 수가 균형을 이루고 있다고 가정 할 근거가 없다. 우리는 실제 응용에서 인물당 예상되는 이미지 분포에 대한 사전 지식이 없는 가운데 전체 LFW 데이터 세트를 클러스터링 한다.
우리는 기준으로 k-means 클러스터링을 고려할 수 있다. 왜냐하면, 가장 잘 알려진 알고리즘이며, 튜닝 할 파라미터가 거의 없고, 가장 효율적이며, 대규모 클러스터링 방법들은 보통 확장성이 향상 된 k-means 클러스터링과 비슷하다. 우리는 MATLAB r2015a의 유클리디안 거리 메트릭 기반 k-means 알고리즘 구현을 사용하였다. 우리는 추가적으로 그래프이론 문제 접근 방식인 spectral 클러스터링("A tutorial on spectral clustering")도 기준으로 사용하였다. 상위 200 개의 이웃을 0이 아닌 값(이 값은 지역 구조를 포착하는데 효과적임)으로 유지하고 다시 유클리드 거리를 사용하여 인접 행렬에 그래프 구조를 유도한다. 클러스터의 개수 C는 반드시 지정되어야 한다. 우리는 MATLAB의 spectral clustering 구현을 사용하였다.
추가적으로 우리는 original Rank-Order 알고리즘을 구현하여 기준으로 사용하였다.
k-means 및 spectral 클러스터링의 경우 알고리즘은 고정 된 클러스터의 수를 매개변수로 요하며, Rank-Order 클러스터링의 경우 클러스터의 수는 거리 임계 값 매개 변수에 따라 달라진다. 실제 응용 프로그램에서는 실제 클러스터 수를 선험적으로 추정 할 수 없으므로 실제 클러스터 수를 결정하는 유효한 절차가 없으므로 모든 알고리즘을 여러 가지 유효한 C 값으로 간단히 평가하고 최상의 결과를 리포트 한다.
k-means와 spectral 클러스터링에 대해 ID숫자와 C가 비슷한 경우 클러스터링 성능과 F-measure는 굉장히 나쁘다.(이러한 알고리즘은 고도로 불균형 한 데이터를 잘 처리 할 수 ​​없으므로 예상 할 수 있다). 이러한 이유로, F-measure의 관점에서 C의 최적값은 상대적으로 낮다. Rank-Order 클러스터링의 경우, 전반적으로 가장 좋은 F-measure값을 유도하는 거리 임계 값은 ID 개수에 가까운 클러스터를 생성하며, 전반적인 F-measure값은 spectral이나 k-means 클러스터링 결과보다 현저하게 높다.
표 2에 따르면, spectral 클러스터링은 단지 LFW의 13,233 개의 얼굴 이미지에 대해서 조차도 계산시간이 현저하게 소요되는 반면, 제안 된 Rank-Order 클러스터링은 상당히 빠르다. 그림 7에 몇개의 클러스터 예가 있다. 인물의 ID 관점에서 (a)와 (b)는 pure 클러스터이고, (c)와 (d)는 impure 클러스터이다.
(c) 클러스터에서, 서로 다른 인물의 3장의 이미지가 다수의 사진이 있는 인물(Walter Mondale)과 그룹화됐다. 반면에 (d)클러스터에서는 1명에 대한 2장의 이미지가 다수의 사진이 있는 인물(Michael Douglas)과 그룹화 되었다.
## Approximation Performance
클러스터링 정확도와 실행 시간 측면에서 k-NN 근사법의 성능을 평가한다. 전체 k-NN 그래프를 계산하기위한 두 가지 근사법을 고려하고 모든 쌍 비교를 수행하는 brute-force방식과 그 성능을 비교한다. 전체 LFW 데이터셋과 여기에 백만개의 unlabeled webface를 더한 데이터셋 각각에 대한 세가지 NN 계산 method의 결과가 표 에 나와있다. 실제로, randomized k-d 트리 방법("Optimised kd-trees for fast image descriptor matching")은 3 가지 방법 중 가장 좋은 실행 시간과 최상의 클러스터링 정확도를 달성했다.
This is a surprising result, since an approximation method
would generally be expected to give less accurate results than
the process it is approximating;
근사법은 일반적으로 근사 된 방법 보다 정확도가 떨어질 것으로 예상되기 때문에 이는 놀라운 결과이다.
 however, since our objective is
to perform clustering based on the nearest neighbor lists, rather
than simply find the exact k nearest neighbors for each item, this
counter-intuitive result can be explained as follows.
그러나 우리의 목적은 각 항목에 대해 정확한 k개의 가장 가까운 이웃을 단순히 찾는 것이 아니라, NN리스트를 기반으로 클러스터링을 수행하는 것이기 때문에 이 반 직관적 인 결과는 다음과 같이 설명 할 수 있다.
Figure 8 plots the number of times (each face in the LFW dataset occurs in the top 200 nearest neighbor list of every face in the dataset).
그림 8은 LFW의 데이터셋에 있는 각 얼굴이 다른 모든 얼굴의 200위 내의 NN리스트에 몇번 등장하는지 나타낸다.
For the exact nearest neighbors, there are a number of face images which occur very frequently in the nearest neighbor lists (up to over half of all nearest neighbor lists), while for the approximate nearest neighbors these faces occur less frequently. 
정밀한 NN에 대해, NN리스트들 (모든 가장 가까운 이웃리스트들의 절반 이상)에서 매우 자주 발생하는 다수의 얼굴 이미지들이 있고, 가장 가까운 이웃들에 대해서는 이러한 얼굴들이 덜 자주 발생한다.
From the perspective of clustering based on the nearest neighbor lists, the lists computed
from the randomized k-d tree approximation actually form more
discriminative features, since certain faces are not present in very
large fractions of the nearest neighbor lists, as is the case with the
exact nearest neighbors.

    가장 가까운 이웃리스트에 기초한 클러스터링의 관점에서 보면, 무작위 화 된 kd 트리 근사화로부터 계산 된리스트는 실제로 정확한 얼굴의 경우와 같이 가장 가까운 이웃리스트의 매우 큰 부분에 특정 얼굴이 존재하지 않기 때문에 더 분별적인 특징을 형성한다 가장 가까운 이웃.
	
	
	
Generally, the randomized k-d tree algorithm has O(n log n)
expected run-time for tree construction, and performing n
searches. In practice, the FLANN implementation of the
algorithm is parametrized with the number of randomized trees
constructed, as well as the total number of nodes available to
visit per search. If fixed parameters are used, the total runtime is
indeed O(n log n); however, if either the number of indices built	
or search size is increased with larger dataset size, the effective
runtime of the algorithm will increase. In practice, we construct 4
trees per index (and have found little impact from using slightly
higher or lower values), but the number of nodes visited per
search must be selected with care. One primary question is to
determine if a fixed number of node visits per search is feasible
for larger datasets, or if the number of nodes visited per search
should increase with dataset size. Table 4 presents results for
clustering based on the LFW dataset, the LFW + 1M dataset, and
the LFW + 5M dataset, using different strategies for selecting the
number of nodes visited per search on the LFW + 5M dataset. In
practice, using the same number of nodes visited per search on the
LFW + 5M dataset as was used on the LFW + 1M dataset leads to
a drastic reduction in clustering accuracy on the larger dataset. In
fact, even a logarithmic increase in search size leads to significant
accuracy loss, relative to a linear increase in search size. In
the following large-scale experiments, we therefore increase the
search size linearly with dataset size. In practice, this means the
run-time of the approximation algorithm cannot be considered to
be O(n log n), since we increase the cost of each search linearly
with the dataset size n, giving a full O(n 2 ) cost for performing n
nearest neighbor searches.

By using the randomized k-d tree algorithm for approximate
nearest neighbor computation, with our updated clustering algorithm
we get improved runtime in the clustering step, and also
better clustering accuracy (compared to the baseline algorithm).
Although we still have an O(n
2
) run-time for the nearest neighbor
computation step, there is still a significant reduction in run-time,
an improvement by a factor of 120 for the LFW+1M image dataset
over brute-force computation.
