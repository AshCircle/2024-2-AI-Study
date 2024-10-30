# Weekly I Learned 4

## Loss Function & Oprimization

### Loss Function

Image Classification에서, Weight Matrix는 입력된 이미지를 정확하게 분류하기 위하여 사용되었다. 이 Matrix의 분류 정확도 향상을 위해, 모델의 예측값과 실제 값의 오차를 반영하여 Matrix를 갱신해야 한다. **Loss Function**은 이때 반영되는 오차를 수치화한다.

- **MSE** (*Mean Squared Error*)

    회귀 문제(*Regression Task*)에서 사용.<br>예측된 값과 실제 값 간 차이를 측정하기 위해 사용한다.

- **SVM Loss** (*Support Vector Machine Loss*)

    분류 문제(*Classification Task*)에서 사용.<br>허용 가능한 오류 범위 내에서 margin을 최대화한다.

- **Cross Entropy Loss**

    분류 문제(*Classification Task*)에서 사용.<br>예측된 확률 분포와 실제 분포 간 차이를 측정하기 위해 사용한다.

### 정규화 (*Regularization*)

**Regularization**은 **Overfitting** 문제를 해결하기 위해 사용하는 기법이다.

- **Overfitting**이란?

    모델이 훈련 데이터에 너무 가깝게 맞춰져 새 데이터에 대한 대응이 어려워지는 현상이다. 이러한 모델은 복잡해서 연산 성능이 떨어지고, 데이터들의 일반화 능력이 낮아지게 된다.

- L1 Regularization

    L1 정규화는 가중치의 절댓값 합을 최소화한다. 가중치가 0을 많이 가질 수 있도록 하여 덜 중요한 특성들은 제거하고 간결한 모델을 만든다.

- L2 Regularization

    L2 정규화는 가중치의 제곱 합을 최소화한다. 가중치가 클수록 더 큰 패널티를 부과하여 모든 특성이 적당히 기여할 수 있도록 만든다.

### 최적화 (*Optimization*)

모델이 더 좋은 결과를 도출하기 위해서는, Loss를 최소화하는, 즉 Loss Function을 줄이는 **Optimization**이 필요하다. 

- **경사하강법** (*Gradient Descent*)

Loss Function의 기울기를 계산해 그 방향으로 Weight를 업데이트 하는 방법이다. 최소지점으로 가는 것이 목표이므로 가장 가파르게 감소하는 방향으로 진행해간다.

- **Learning Rate Scheduler**

학습 초기에 높은 학습률을 사용하여 최적점 근처로 접근하고, 점진적으로 학습률을 줄여가는 방식이다. 이는 Loss Function의 지역 최소값을 벗어나 전역 최소값으로 가는데 도움을 준다.