# Weekly I Learned 5

## Backpropagation and Neural Network

### Backpropagation과 계산 그래프

역전파(*Backpropagation*)는 예측값을 통해 얻은 오차를 역방향으로 전파하며 노드의 가중치를 조정하는 과정이다.

Backpropagation 과정에서 입력을 x, 출력을 y라고 하면, 한 layer를 통과할 때 일어나는 과정을 f(x) = y 라는 식으로 나타낼 수 있다. Loss function은 layer가 굉장히 많기 때문에 함수 f 또한 굉장히 많이 중첩된 합성함수 꼴을 띄게 된다.

상기한 이유로, Backpropagation 방법을 쓰지 않는다면 n개의 가중치에 대해 별도로 손실을 계산해야 하므로 총 n번의 계산이 필요하다. 그러나 Backpropagation 방법을 사용하면 미분 연쇄 법칙(*Chain Rule*)을 통해 1번의 계산으로 모든 가중치의 기울기를 동시에 구할 수 있다.

- **계산 그래프의 역전파**

$f(x) = y$, $g(y) = z$ 꼴의 계산 그래프가 역전파 과정을 거친다고 하자. 미분 연쇄 법칙에 의해, $z$에서는 $\frac{\partial z}{\partial z}$, $y$ 에서는 $\frac{\partial z}{\partial z}\cdot\frac{\partial z}{\partial y}$ 꼴일 것이고, $x$ 에서는 $\frac{\partial z}{\partial z}\cdot\frac{\partial z}{\partial y}\cdot\frac{\partial y}{\partial x}$ 꼴일 것이다.

- **덧셈 노드의 역전파**

$x$와 $y$에 대해 덧셈 연산을 하여 $z$을 만드는 노드에 대하여, $z$까지 이루어진 역전파에 의해 $\frac{\partial L}{\partial z}$가 미분값으로 존재한다고 하자. 이때 $x$에서의 미분값은 $$\frac{\partial L}{\partial z}\cdot\frac{\partial z}{\partial x} = \frac{\partial L}{\partial z}\cdot\frac{(x + y)}{\partial x} = \frac{\partial L}{\partial z}\cdot1 = \frac{\partial L}{\partial z}$$의 결과를 가진다. 입력값을 그대로 흘려보내주기 때문에 *gradient distributor* 라고도 표현한다.

- **곱셈 노드의 역전파**

$x$와 $y$에 대해 곱셈 연산을 하여 $z$을 만드는 노드에 대하여, $z$까지 이루어진 역전파에 의해 $\frac{\partial L}{\partial z}$가 미분값으로 존재한다고 하자. 이때 $x$에서의 미분값은 $$\frac{\partial L}{\partial z}\cdot\frac{\partial z}{\partial x} = \frac{\partial L}{\partial z}\cdot\frac{(x \cdot y)}{\partial x} = \frac{\partial L}{\partial z}\cdot y$$의 결과를 가진다. 입력값의 위치를 바꿔서 곱해 흘려보내주기 때문에 *gradient switcher* 라고도 표현한다.

결론적으로 Backpropagation 과정을 통해 얻은 미분값을 통해, 파라미터 값의 변화가 최종 Loss에 주는 영향이 얼마만큼인가를 알아낼 수 있다.