# Weekly I Learned 8

## Attention Mechanism

**어텐션(*Attention*)** 이란, 인간의 "주의"과 유사한 개념을 NLP 또는 Computer Vision에 도입한 것이다. 입력 데이터 일부에 더 가중치를 더 높게 주자는, 즉 중요한 데이터에 더 집중하도록 하자는 아이디어에서 출발했다.

### NLP(*Natural Language Processing*)에서의 Attention

텍스트를 출력하는 seq2seq 모델은 입력 문장이 길어지면 초기 단어의 영향력이 떨어지는 문제가 발생한다. Attention과 함께라면, 출력 단어를 예측하는 매 시점에 전체 입력 문장을 다시 참고한다. 단, 더 연관된 부분에 Attention score를 더 높게 주어 더 집중해서 보도록 한다.

### Computer Vision에서의 Attention

**ViT(*Vision Transformer*)** 는 NLP의 Transformer 모델을 Computer Vision에 적용한 사례이다. 이미지를 패치 단위로 분할 후 Self-Attention Mechanisim으로 모든 패치를 참조하여 전역적 관계를 학습한다.

CNN보다 ViT가 대규모 데이터셋에서 더 강력한 성능을 발휘하나, O(n)의 시간복잡도를 가지는 CNN과 달리 ViT는 각 패치가 전체를 참조하기 때문에 O(n^2)의 시간복잡도를 가진다. 따라서 느린 속도 문제로 처음엔 잘 사용되지 않았지만, 최근엔 pretrained 된 ViT 모델이 많아져서 ViT를 쓰는 추세가 높아졌다.