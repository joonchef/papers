초광각 안저영상에서 동맥/정맥 분류를 위한 그래프컷 접근

혈관을 동맥류와 정맥류로 분류하는 것은 전신 질환에 대한 망막 생체 지표의 자동 조사의 기본 단계이다.
이 논문에서는 스캔 레이저 ophthalmoscope를 사용하여 획득한 레티날 펀드의 초광각 영상에 혈관 분류를 위한 새로운 기법을 소개한다.
우리가 알고 있는 한, 수동 개입이 없는 망막 영상의 이러한 유형에 대해 완전히 자동화된 artery.vein 분류 기법이 발표된 것은 이번이 처음이다. 제안된 방법은 국소 혈관 강도 및 혈관 형태학에 기초한 수동 조작 특징을 이용하여 동맥과 혈관 네트워크 간의 세계적인 최적의 분리를 그래프 절단 접근법으로 계산하는 그래프 표현을 만듭니다.
이 기법은 세개의 서로 다른 데이터 세트(하나는 공개적으로 사용 가능하고 두개는 로컬)에서 테스트되었으며 가장 큰 데이터 세트에서 평균 분류 정확도 0.883을 달성했습니다.

컴퓨터화된 영상 양식의 영상 기관은 임상 의사가 눈과 전신 질환의 조사를 위해 망막의 디지털 고해상도 영상의 양을 증가시키는 것을 가능하게 했다. 망막에서, 인체의 미세 조직의 풍부한 부분이 비침투성으로 관찰될 수 있다. 따라서, 망막 현미경의 특징들과 그것들의 변화들은 생체 지표 후보로서 조사되어 왔다.
심혈관 질환, 치매, 당뇨병과 같은 다양한 유형의 신체적 조건과의 연관성[1] 전신 질환에 대한 망막 생체 측정기 연구는 전통적으로 안더스 카메라 영상에서 관찰된 광학 디스크를 중심으로 한 작은 원형 고리 모양의 고리 모양의 고리로 제한되어 왔습니다[6–[9]. 확장된 망막 영역(45°를 초과)의 단일 영상 획득은 반복적인 획득과 마운트를 통해서만 가능했으며, 주된 예는 ETDRS(초기 치료 당뇨 치료 스터디)프로토콜입니다.
당뇨병 망막증 스캔 레이저 ophthalmoscope(SLO)[11]의 도입으로 한번의 촬영으로 촬영할 수 있었습니다(그림). 1)180-200°의 초광각 시야를 가진 영상[12], 양호한 영상 해상도를 보장하면서 환자 불편을 줄인다. 측정 기능을 제공하는 자동 시스템
생물학적 지표 연구를 위한고, 작은 레티날 혈관은 동맥이나 정맥류로 안정적으로 분할 및 분류되어야 한다. 이 작업은 수동으로 수행하는 경우 시간이 많이 소요되므로 효과적으로 수행할 수 있는 소프트웨어 도구를 개발하는 것이 매우 중요합니다.

동맥/정맥에 대한 새로운 자동화 기술을 제안합니다.
(AV)영상에 표시되는 망막 혈관의 분류. 먼저 선박 중심선을 따라 수동으로 제작된 형상을 추출하고 AV라벨을 픽셀 레벨에서 먼저 추출한 다음 세그먼트 레벨에서 추출할 수 있는 로컬 분류자를 교육합니다. 그런 다음 혈관 세그먼트의 네트워크 표현을 방향이 지정되지 않은 그래프로 계산하고 글로벌 수준에서 라벨이 일관되게 확산되도록 네트워크를 분할하여 분류 정확도가 크게 향상됩니다. 이것은 소설을 사용함으로써 얻어진다.
그래프 절단 접근법을 위한 소프트 제약 조건과 에지 비용의 공식화, 전체 혈관 구조 네트워크 전체에 분기 및 교차점 구성을 반대하는 것을 목표로 한다.

제안된 방법의 장점은 다음과 같습니다.
•수동 조정이 없는 상태에서 실제고 있는 것으로부터 완전히 자동으로 계산된 입력 불완전 바이너리 혈관 맵으로 수락한다. 우리가 가장 잘 알고 있는 바로는, 해당 주제에 대해[13]에 대해고 보고된 유일한 다른 비교 가능한 시스템은 수동으로 지정된 중심선 맵에서만 검증되었다.
•용기 경로를 따라 라벨 불일치를 최소화하기 위해 전역적으로 최적화된 AV라벨 표시가 적용됩니다.
•혈관 형태 측정학의 국부적 특성에 기초한 고정 규칙은 교차점과 분기점을 분리하도록 사전 설정되어 있지 않다. 대신 이 단계를 수행하기 위한 매개 변수는 별도의 영상 세트에서 최적화되었습니다.
•유사한 연구에서처럼 고정된 연역적 규칙에 따라 설정하는 대신 그래프 가장자리 분류 단계에서 분기 및 교차점 형태와 혈관 로컬 모양에 관한 정보를 동시에 결합하여 활용합니다[14].
우리가 알기로는, 자동으로 생성된 혈관 분할에서 시작하여, 직접 생성된 것을 시작하여,고 있는 것은 이번이 처음이다.

일반적인 펀드 카메라 이미지의 AV분류를 위해 몇가지 자동화된 기술이 제안되었다. 개별 단계는 방법마다 상당히 다르지만 대부분의 접근 방식에서 네가지 주요 단계를 확인할 수 있다. 먼저 자동 또는 수동 도구를 사용하여 혈관이 분할됩니다. 둘째, 혈관의 중심선을 추출하기 위해 결과적으로 생성되는 바이너리 맵이 사전에 처리되고 경사 처리됩니다. 셋째, 각 중심선 픽셀에서 로컬 형상 세트가 계산된다. 넷째, 형상 벡터는 감독되거나 감독되지 않은 접근 방식을 통해 픽셀을 분류하는 데 사용되며, 결과 라벨은 전체 혈관 세그먼트에 대한 라벨을 얻기 위해 결합됩니다.
잘 알려 진, Grisan과 Ruggeri에 의한 초기 연구[15]는 약물 측정기 주위의 작은 원형 영역에서 이 과제를 다루었다.
저자들은 분할 외 임피던스 전략을 활용하고 두가지 색상 특성만 선택하여 주 선박에 대한 분류 정확도 0.93을 얻었다. 특징들의 군집화에 기반한 유사한 접근법이 Va.uez 등에 의해 제안된 후[16]에 의해 확장되었으며, Saez등이 혈관 단면적 프로파일을 대표한다.
컬러 기능은 또한 AV분류를 위한 감독되지 않는[18]및 감독되지 않은[19]알고리즘에도 사용되었습니다. Niemeijer의 방법은 단일 픽셀에서 추출한 더 큰 기능 집합, 문제의 혈관 픽셀 및 혈관 세그먼트를 중심으로 관심 영역(ROI)을 탐색했습니다. 그런 다음 특성 선택을 수행하고 다양한 분류기를 테스트하여 어떤 것이 최상의 성능을 제공하는지 평가했습니다.
우리는 '잠페리니'가 쓴 종이 위에 손으로 만든 큰 특징들을 고안해 냈습니다.
에 제안된 프레임워크에서 다른 색상 공간(RBG및 HSV)의 채널에서 강도 값과 1차 및 2차 지수 모멘트가 계산되었다.
값은 두번 추출되었습니다. 먼저 해당 픽셀 중심의 ROI에서 직경이 해당 지점의 혈관 폭과 같고, 그 다음에는 이전 ROI보다 두배 큰 ROI에서 추출됩니다. 또한 픽셀의 위치에 관한 정보는 분류 정확도를 향상시키는 것으로 보였다. 마지막으로, 특징 선택이 수행되었고 여러 유형의 분류자가 교육을 받았다. 최상의 결과를 얻은 것은 선형적인 베이지안 분류기(LBC)였다[23].

보다 최근에는, 추가적인 차별적 정보를 얻기 위해 전체 혈관 구조의 특성이 고려되었다. 분할된 바이너리 맵의 혈관의 정확한 표현과 모호한 분기점과 교차점의 구분은 Al-Dirietal.[24]및 Hungetal.[25]에 의해 조사되었습니다. 그러나 이 두 논문에서 그 결과는 AV분류 면에서 평가되지 않았다. AV분류 목적으로 특별히 설계된 그래프로서 혈관 구조의 첫번째 표현은 Rothausetal.[26]이 제안한 반자동 그래프였습니다. 이 경우, 두개의 쌍을 이룬 그래프가 고안되었고, 알고리즘에 의해 해결된 라벨 분쟁 측면에서 결과를 평가했다. 최근에는[13],[14]및[27]–[31]중에서 AV분류 문제를 다루기 위해 그래프 표현을 제안하는 연구가 증가하고 있습니다. 에스트라다는고 있었다. 이 기법은 해부학적으로 타당한 혈관 네트워크의 공간을 탐색하기 위해 경험적 최적화 알고리즘을 기반으로 동일한 저자들의 이전 논문의 확장이다. 이러한 각 구성에 대해 혈관 트리 기능을 기반으로 하는 글로벌 가능성 모델이 개발되었습니다. 이러한 접근 방식에서 혈관 구조는 그래프로 표현되며 제안된 AV라벨이 혈관 트리 전체와 영상의 전체 FoV에서 일관되게 유지되도록 하기 위해 활용됩니다. Joshi등[14]은 혈관 분할과 분기점과 교차점에서 혈관 세그먼트가 연결된 정밀 중심선 지도 작성으로 시작했습니다. 그들은 그래프의 노드로 세그먼트를 모델링하고 지역 특성에 기초한 가중치 세트를 그래프 가장자리에 할당했습니다. 그런 다음 Di.stra 알고리즘을 사용하여 그래프의 파티션을 얻었습니다. 라벨은 픽셀 수준에서 추출한 4-D형상 벡터 집합의 퍼지 2-평균 군집화를 사용하여 그래프 구성 요소에 지정되었다. 벡터 구성 요소는 네가지 색상 특징(녹색 채널 및 색조의 평균 및 표준 편차)으로, 고려된 제반 부품 카메라 이미지에서 매우 차별적인 것으로 판명되었습니다. 매우 불확실한 AV라벨을 가진 픽셀을 제외하는 것이 데이터의 대다수를 제거하게 되었을 것이기 때문에는 것으로 간주되었다는 것을 관찰하는 것은 흥미롭다. 마지막으로 Dashtbozorg등의 기술[28]은 시행 중인 전처리 단계에 대한 이 작업에 관련이 있었다. 나머지 작업은 그래프 분할 문제로 AV분류를 모델링 하는 측면에서 Joshi등의 작업과 유사했습니다. 가장 주목할 만한 차이점은 경험적으로 정의된 규칙 집합에 따라 모든 교차점과 분기점을 순차적으로 해결함으로써 실제적인 분리가 이루어졌고 로컬 AV라벨은 더 큰 특징 벡터를 생성합니다. 사전 처리는 중심선 지도에서 볼 수 있는 분할 오류를 수정하는 데 사용되는 일련의 고정 규칙으로 구성되었습니다. 이러한 경험적 규칙은 혈관 세그먼트의 로컬 특성을 결합하여 얻은 임계값을 기반으로 했습니다. Dashtbozorg등에 의한 작업은 문헌에 제안된 몇 안 되는 그래프 기반 알고리즘 중 하나이며[13]에서 수동으로 획득하거나 개량하지 않은 중심선 맵에서 신뢰성 있게 수행한다.

