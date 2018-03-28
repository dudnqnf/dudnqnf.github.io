---
layout: post
title: "ML_note #4 CNN"
date: 2017-12-22
excerpt: "Machine Learning"
tags:
- Deep Learning
ref:
- 김성훈 교수님의 온라인 강의 및 논문
- 밑바닥부터 시작하는 딥러닝
- https://github.com/WegraLee/deep-learning-from-scratch
comments: true
---
# Convolutional Neural Network(CNN)

#### 개요
- Convolution : 행렬 합성곱
- 사람의 이미지 추상화방법 + DNN(Deep Neural Net.) 조합
- 영상 이미지 인식 기술에 좋은 성과를 보이고 있는 알고리즘
- 이미지(10 * 10 * 3 행렬, 입력)에 대한 정답(1~9의 숫자 중 택1, 출력)을 통해서 필터(W, 가중치)와 편향값(b)를 학습하는 모델

#### 이미지 추상화
- 사람의 추상화 = 이미지를 픽셀단위로 기억하지 않고 특징을 추상화하여 기억
- CNN의 추상화 = 필터를 통해 특징만 남은 이미지를 학습

#### 새로운 용어
- feature map : 입/출력 이미지(X/Y)
- filter : 가중치(W) / 학습대상
- stride : 필터를 한번에 몇 칸씩 옮길지
- padding : 이미지의 경계부분에 추가적인 0으로된 행렬 추가 / 결과값의 행렬크기 조정에 필요
- channel : 필터, 입력데이터의 두께(층수)

**입력과 출력크기 관계**<br>
입력크기(H, W), 필터크기(FH, FW), 출력크기(OH, OW), 패딩(P), 스트라이드(S)<br>
$OH = \frac{H+2P-FH}{S}+1$<br>
$OW = \frac{W+2P-FW}{S}+1$
{: .notice}

#### 새로운 레이어
- Convolution Layer : 이미지(x) * 필터(W) 가 일어나는 layer
- Pooling Layer : max(x)

#### CNN 네트워크의 예
conv -> relu -> pooling -> conv -> relu -> pooling -> conv -> relu -> Affine -> relu -> affine -> softmax

**TIP**<br>
relu는 선택<br>
{: .notice}

#### 예측 (FowardProp)
- layer1(conv)
  - input feature map : arr = (10, 3, 10, 10) # 배치사이즈, 채널, 행, 열
  - filter : arr = (5, 3, 3, 3) # 필터개수, 채널, 행, 열
  - stride = 1
  - padding = 1
  - feature map * filter
    - 필터가 (0, 0)부터 stride의 크기만큼 이동하면서 합성곱
    - 채널별로 진행
    - 결과(output feature map) : arr = (10, 5, 10, 10)
- layer2(relu)
  - 행열의 모든 요소에 활성화함수 적용
  - 결과 : arr = (10, 5, 10, 10) # 변함없음
- layer3(pooling)
  - pooling size = (2, 2) 라고 가정
  - 입력데이터의 size가 pooling size의 정수배가 되도록 설정
  - 결과 : arr = (10, 5, 5, 5) # 행열 사이즈 변화
- ...
- layer9(Affine)
  - 행열내적(output개수 = 2로 가정)
  - input : arr = (10, 300) # 배치사이즈, 채널 * 행 * 열
  - W : arr = (300, 2)
  - output : arr = (10, 2) # 배치사이즈, output개수
- layer10(softmax)
  - 각각의 output에 대해서 softmax함수 적용

**TIP**<br>
입력데이터의 채널 = 필터 채널<br>
filter의 개수 = 출력데이터의 채널<br>
{: .notice}

#### 학습 (BackProp)
- layer10(softmax  + cross_entropy) : 미분값 = y - t
- layer9(Affine) : 행열내적 미분과 동일
- ...
- layer3(pooling) : 학습에 관여 안함
- layer2(relu) : 미분값 = 0 or 1
- layer1(conv) : 행열내적 미분과 동일

**im2col**<br>
행렬을 내적하기 좋은 행태로 변형할 때 자주 사용되는 함수. 입력데이터는 배치데이터 하나당 가로로 한 줄, 필터셋은 필터 하나당 세로로 한 줄(필터 하나를 여러번 곱해서 길게 만든 한 줄). 내적을 하여 출력데이터(2차원)를 생성하고 reshape을 출력데이터 생성.
{: .notice}

#### 대표적인 CNN
- LeNet
  - 손글씨 숫자를 인식하는 네트워크
  - 20년전에 처음 제안된 CNN
  - LeNet에서 이용되는 sigmoid함수와 서브샘플링은 현재 ReLU와 최대 풀링으로 대체되어 이용됨

- AlexNet
  - 활성화 함수로 ReLU를 이용
  - LRN이라는 국소적 정규화를 실시하는 계층을 이용
  - 드롭아웃을 사용

- VGG
- GoogleLeNet
- ResNet
- ...

#### 정확도 향상
- 데이터 확장 : 데이터의 개수가 부족할 때 한 개의 데이터를 회전 및 이동을 통해서 다양한 데이터 셋을 만들어 낼 수 있음
- 다층구조 : 한 번에 큰 필터를 적용하여 연산 하는 것보다 작은 필터를 여러번 연산하는 것이 연산량이 적음
