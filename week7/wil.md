# Weekly I Learned 7

## Object Detection

**객체 탐지(*Object Detection*)** 란, 이미지에서 어떤 객체가 어느 위치에 있는지를 파악하는 Task이다. 이 Task는 해야 하는 일이 크게 두가지로 나뉘는데, 먼저 이미지에서 임의의 객체들을 파악하고 각 객체들의 Bounding Box 정보를 통해 위치를 알아내는 **Localization**이 있으며, 이후 이 Bounding Box에 속한 객체에 대하여 class를 분류해주는 **Classification**이 있다.

이미지의 Feature Map을 통해 객체 탐지를 진행하며 몇 단계를 걸치는지에 따라, Two-Stage Detector와 One-Stage Detector로 구분할 수 있다.

### Two-Stage Detector

Feature Map에서 먼저 Region Proposal, 즉 NMS 처리를 한 후, 가장 높은 score의 Bounding Box에 대해서 Box의 크기를 세밀하게 보정함과 동시에 Classification을 진행한다. 즉, 객체의 대략적인 위치를 찾아내는 Stage와 그 영역을 보정하고 객체 분류를 진행하는 Stage로 나뉜다.

여기서 NMS(*Non-Max Suppression*)란, 여러 후보 BBox에 대해서 동일한 객체를 가리키는 BBox를 제거하는 기법을 말한다. 이 때 동일한 객체인지 판단하는 지표는 IOU(*Intersection Over Union*)로, 두 Bounding Box의 면적이 얼마나 겹치는지를 나타낸다.

- **R-CNN(*Region-Based CNN*)**

    Selective Search 알고리즘을 통해 여러 ROI(*Region of Interest*)를 뽑고, 각 Region을 고정된 크기로 warping 한 후 SVM Classification 및 BBox regression을 진행한다.

    그러나 ROI를 2000개 가량 추출하기 때문에, CNN 또한 2000번 거치게 되어 너무 계산 비용이 크다는 단점이 있다.

- **Fast R-CNN**

    ROI를 뽑고 각각 CNN을 거친 R-CNN과 다르게, 먼저 CNN을 한번만 통과시켜 Feature Map을 얻고 ROI Pooling을 통해 해당 객체의 Class와 BBox값을 얻는다.

    CNN을 한번만 거치기 때문에 R-CNN 방법보다 속도가 빠르다는 장점이 있다.

    - ROI Pooling이란?

        R-CNN의 warping은 고정된 크기로 동작하기 때문에 원 정보 손실로 좋은 성능을 보장하기 힘들다. ROI Pooling은 이를 개선하여 원 ROI 비율을 유지하기 때문에 더 나은 성능을 보장한다.

- **RPN(*Region Proposal Network*)**

    다양한 종횡비를 가질 수 있는 Anchor Box 개념을 도입하여, 앵커 박스 안에 객체가 있는지 없는지 판단하고, 객체가 존재한다면 객체의 중심을 찾아 Bbox를 resize한다.

- **Faster R-CNN**

    Fast R-CNN에 Selective Search 대신 RPN을 적용한 모델이다.

### One-Stage Detector

Region Proposal 단계 없이 Feature Map에서 바로 Localization과 Classification을 진행한다. 단순하기 때문에 Two-Stage Detector보다 빠르지만 정확도는 떨어진다.

- **YOLO(*You Only Look Once*)**

    이미지를 그리드로 나고, 각 그리드 셀에서 객체가 있는지의 여부를 판단한다. 각 셀은 객체의 좌표와 클래스 확률을 한번에 예측한다.