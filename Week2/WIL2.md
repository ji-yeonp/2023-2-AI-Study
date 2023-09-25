2주차 강의내용 정리

2주차 핵심내용
1. Segmentation
2. Object Detection
3. Pytorch
   
   
1. Segmentation
   이미지를 픽셀별로 분류해 사람/벽/나무 등으로 분류하는 semantic segmentation과, 같은 클래스여도 인스턴스마다 분류해 사람1/사람2, 자동차1/자동차2 등으로 도출하는 instance segmentation 총 두 종류가 존재한다.

   CNN은 convolution과 pooling을 반복해 이미지 분류에 많이 사용되었다. 그러나 시간이나 비용 등 기존의 CNN의 문제를 개선하기 위해 FCN이 대두되었고, FCN을 통해 segmentation이 발전하였다.

   Fully Connected Layer은 convolution을 반복하고, 이름 뜻 그대로 하나의 output을 출력하기 위해 모든 input을 사용해야 한다는 문제가 있었다. 이는 자연스럽게 Fully convolutional Network로 대체되었다. 둘의 차이점은 FCN은 input과 똑같은 크기의 output을 생성 가능하다는 것, convolution 연산으로 공간값을 보존할 수 있다는 것이다.

   Upsampling은 연산을 거듭할수록 디테일해지는 deconvolution과 화질이 좋아지는 보간법 두 가지 방법이 존재한다. Pooling과 반대되는 과정이어서 Unpooling이라고 불리기도 한다. Convolution과 Pooling을 거듭하며 원본 이미지를 압축해나가는 것과 반대로 그 크기를 늘려나간다.

2. Object Detection
   Object Detection은 bounding box로 객체의 위치를 찾는 태스크를 의미한다. Bounding box란 박스 모양으로 어떠한 이미지에서 그림을 보존하는 방법이다.

   Object Detection은 여러 방법이 존재하고, 가장 먼저 나온 것은 R-CNN이다. R-CNN은 selective search라는 탐색법을 통해 이미지에서 2,000여개의 패치를 발견한다. 이 패치를 일정한 크기로 조절하고, 여기서 feature값을 추출해 이 값을 classify해 수행한다. 알렉스넷을 패치의 개수만큼 수행해야 해 시간이 많이 걸린다는 단점이 있다.

   SPPNet은 R-CNN과 달리 한 번의 CNN으로 해결해 속도를 향상할 수 있다는 장점이 존재한다. Pooling Layer가 여러 개 겹쳐있는 네트워크를 의미하고, input의 이미지 사이즈를 고정시키지 않는다는 것을 목표로 해 feature extractor와 FCN 사이에서 유연하게 움직일 수 있는 별도의 레이어를 추가하였다.

   Fast R-CNN은 R-CNN보단 빨라졌지만 여전히 느리다. R-CNN과 비슷하게 selective search를 사용해 탐색하고, 추출된 패치들을 고정된 feature 값으로 만들기 위해 ROI Pooling을 수행한다.

   YOLO(YoU Only Look Once)는 가장 유명한 방법으로, 현재 버전이 8개 이상 나왔다. 가로 세로를 동일한 그리드 영역으로 나눈 후 각 그리드 영역에 대해 어디에 사물이 존재하는지 신뢰도 점수를 예측한다. 이와 동시에 어떠한 사물인지에 대한 작업을 진행한다. 신뢰도 점수가 높은 박스일수록 사물이 존재할 확률이 높다는 것을 의미해 점수가 높은 박스만을 남기고 전부 제외한다.

3. Pytorch
   Pytorch는 프레임워크의 한 종류이다. 프레임워크란 라이브러리나 모듈을 효율적으로 사용할 수 있도록 묶어 놓은 패키지이고, tensorflow, pytorch, JAX 등이 존재한다. 이 중 pytorch가 배포성이 좋고 유연해 현재 연구 등에서 가장 흔히 사용된다. cuda를 통해 GPU를 사용할 수 있어 CPU를 사용하는 것보다 시간을 단축할 수 있다.

   Pytorch의 작동법 중 하나인 view와 reshape은 둘다 shape 변환이 가능하다는 공통점이 있지만, view는 메모리 주소를 copy하는 shallow copy이고 reshape은 값을 copy하는 deep copy이다. 연산자는 행렬곱이 가능한 mm과 벡터를 내적할 수 있는 dot 등이 존재한다.

   Pytorch를 사용하려면 config.json 파일을 통해 어떠한 변수를 사용할 것이고, 사용할 수 있는 범위는 어디부터 어디인지 등의 환경과 디테일을 설정해주어야 한다. 이렇게 설정된 것들은 python train.py -c config.json이라는 명령어를 통해 사용 가능하다.