# Weekly I Learned 6

## CNN, Activation Function, Batch Normalization

### CNN

FNN(*Fully-Connected Neural Network*)는 인접 픽셀간 상관관계가 무시되기 때문에 이미지 분류에 적절하지 않은 방법이다.

그에 반해 CNN(*Convolutional Neural Network*), 즉 합성곱 신경망은 인접 픽셀간 상관관계를 고려하며 학습하는, 이미지 분류에 적절한 신경망이다.

CNN의 Convoultional Layer에서 하는 작업은 두 가지로 분류할 수 있다.

- **Convoultion Output 추출**

    이미지 일부분과 작은 필터를 합성곱 연산하여 특정 부분의 특징들을 추출한다.

- **Activation Function 적용**

    선행 과정의 Output에 비선형성을 띠는 활성화 함수를 적용하여 더 복잡하고 추상적인 특징을 학습할 수 있도록 한다.

### Batch Normalization

신경망 각 Layer의 입력을 정규화(평균 0, 분산 1)하는 것을 배치 정규화(*Batch Normalization*)라고 한다. 신경망의 Layer 사이에 이를 적용하여, mini-batch(일반적으로 32~256개 데이터)의 입력을 정규화한다.

- **왜 사용하는가?**

    Batch 단위의 학습을 하면, 각 배치의 입력 분포가 계속 변하는 내부 공변량 변화(*Internal Covariant Shift*)가 나타날 수 있다. 이는 매 학습마다 모델이 적응해야 하는 입력의 분포를 다르게 만들어 학습을 느리게 만든다.

    따라서 입력 분포를 유지하여 학습 속도를 빠르게(수렴이 빠르도록) 하기 위해서 배치 정규화를 적용한다.

### Transfer Learning

사전 학습된 모델을 현재 필요한 작업에 재사용하는 방법을 전이학습(*Transfer Learning)이라고 한다.

- **왜 사용하는가?**

    신경망 학습에서 가장 중요한 것은 데이터이다. 그러나 task에 맞는 고품질의 데이터셋을 직접 얻는 것은 너무 많은 비용을 필요로 한다.

    전이학습을 적용하면, 다른 대규모 데이터셋에서 학습한 지식을 현재 필요한 새로운 작업에 쉽게 적용하고, 이러한 데이터 부족을 극복할 수 있다.

- **보유한 데이터 수에 따른 전이학습방법**

    데이터가 거의 없는 경우, 사전 학습된 모델의 가중치를 그대로 사용하고, 마지막 층만 새 작업에 맞게 수정한다.

    데이터가 조금은 있는 경우, 별도의 가중치 동결을 하지 않고, 마지막 층만 새 작업에 맞게 수정한다. 그리고 Convolutional Layers에 더 작은 Learning Rate를 적용한다.
    
    이를 통해 사전 학습된 모델에서 추출한 일반적인 특징들을 새 작업에 적용할 수 있다.

### Knowledge Distillation

지식 증류(*Knowledge Distillation*)란, 큰 모델(*Teacher Model*)을 작은 모델(*Student Model*)로 압축하는 과정을 말한다. 학생 모델은 교사 모델의 출력을 모방하도록 학습되며, 이를 통해 성능을 유지하면서도 배포가 용이한 모델을 만들 수 있다.