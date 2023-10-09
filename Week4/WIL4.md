인공지능 스터디 4주차 WIL

Object Detection: 물체를 감지하는 것
-어떠한 이미지를 투입하면 그 이미지의 레이블을 분류하고 bbox값을 출력한다

Sliding Window
-오른쪽으로 window 한 칸씩 옮기며 window 안에 어떤 이미지가 있는지 찾는다
-객체가 있다면 classification을 진행한다
-1001개의 클래스로 분류한다
-한 번 실행하는 것이 아닌 여러번 반복해 진행한다
*예시로 8px*8px이미지를 2px*2px의 window로 탐색을 진행한다면 이미 지나온 픽셀을 바로 건너뛰는 것이 아닌 계속해서 탐색을 한다
->window의 가로세로 크기를 각각 w', h', 이미지의 가로세로 크기를 각각 W, H라 한다면 탐색횟수는 총 (W-(w'-1))*(H-(h'-1))번
-그러나 이미지 크기가 너무 크다면 감당불가해 이 방법은 실행이 불가능하다

위 방법을 대신하는 방법: 모든 경우의 수 따지는 것이 아닌 객체 포함 확률이 높은 이미지 영역 찾는다(Region Proposal)

R-CNN: Selective Search 알고리즘 사용
1. selective search로 ROI 추출
2. 224*224로 warping
3. CNN feature 계산
4. Linear SVM으로 분류

IOU(Interest Over Union)
-값이 1에 가까울수록 같은 객체 가리키고 있을 확률 높다

NMS(Non-Max Suppresion)
1. 값 내림차순으로 정렬해 가장 높은 값 가진 박스 선택
2. 나머지 박스와 IOU 비교해 0.7이상의 값 가진 박스 제거
3. 반복
*문제: 사진 안에 객체가 많이 겹쳐있으면 좋은 bbox 제거할수도 있음



