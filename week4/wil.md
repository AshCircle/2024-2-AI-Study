# Weekly I Learned 2

## 이미지 분류 (*Image Classification*)

이미지 분류란, 컴퓨터가 이미지를 보고 이미지가 어떤 카테고리에 속하는지 판단하도록 하는 일련의 과정을 말한다.

### 컴퓨터가 이미지를 읽는 방법

이미지 분류를 알기 위해서는 컴퓨터가 이미지를 어떻게 데이터로 받아들이는지 알아야 할 필요가 있다. 이미지 데이터의 구조는 3개로 분류한다.

- **픽셀** (*Pixel*)

    이미지 데이터의 기본단위이다. 픽셀 하나는 하나의 색 정보를 담고 있다.

- **채널** (*Channel*)

    각 픽셀의 색상 정보를 일컫는다. 체계에 따라, 채널의 개수는 달라질 수 있다.

    RGB : 3채널 (Red, Green, Blue)<br>CMYK : 4채널 (Cyan, Magenta, Yellow, Key plate)<br>Grayscale : 1채널

- **해상도** (*Resolution*)

    이미지 데이터가 몇개의 픽셀로 구성되었는지를 나타낸다. 보통 '가로 x 세로'로 나타낸다.

컴퓨터는 이 구조를 활용하여 이미지를 배열, 행렬로 처리할 수 있다.

## FNN과 CNN

### 완전 연결 신경망 (FNN, FCNN, *Fully Connected Neural Network*)

이미지를 1차원으로 펼쳐서 처리하는 신경망이다.

- **한계**

    FNN, 즉 Raw-Pixel 모델은 이미지 분류에 적절하지 않은 방법이다.

    먼저, 불필요한 픽셀(배경 픽셀 등)을 모두 인식 기준에 포함시키기 때문에, 인접 픽셀끼리의 상관관계를 특별하게 여기지 못한다.

    또한, 이미지의 시점 차이, 조명의 변화, 다른 포즈, 피사체 가려짐 등의 환경을 가진 다양한 데이터셋을 처리하기 힘들다.

### 합성곱 신경망 (CNN, *Convolutional Neural Network*)

이미지를 2차원 구조를 유지하며 처리하는 신경망이다. FNN과 달리, 인접 픽셀간 관계를 고려하며 처리하기 때문에 라벨의 특징을 잘 학습할 수 있다. 즉, 다양한 데이터셋에서도 강건한 분류가 가능하다.

- **Convolutional Layer**

    이미지에 다양한 필터를 적용하여 특징을 추출하는 계층이다. Convolution Output 추출 과정과 Activation Function 적용 과정으로 나눌 수 있다.

    - Convolution Output 추출

        이미지 일부분과 작은 필터를 합성곱 연산하여 Feature Map을 얻는다. 가령 `N x N` 행렬에 `k x k` 필터를 적용한다면, `(N - k + 1) x (N - k + 1)` 행렬을 얻을 수 있다.

    - Activation Function 적용

        모델이 더 복잡하고 추상적인 특징을 학습할 수 있도록, Feature Map에 Activation Function을 적용하여 비선형성을 추가한다.

- **Pooling Layer**

    Feature Map의 크기를 축소하는 계층이다. 이를 통해 앞으로의 연산량을 줄일 수 있으며, 중요한 특징만 남겨서 모델이 이미지의 위치 변화에 강건해지도록 학습시킨다.
    
    주로 Max Pooling을 사용하는데, 이는 영역에서 가장 큰 값을 선택하는 방식이다. 다른 방식으로는 Average Pooling이 있으며, 이는 영역의 평균값을 계산하는 방식이다.

- **Fully Connected Layer**

    Convolution Layer, Pooling Layer를 반복하여 얻은 output을 flatten하여 최종 분류를 수행한다. 최종 output은 각 클래스에 속할 확률을 담고 있다.