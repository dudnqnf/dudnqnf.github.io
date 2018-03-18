---
layout: post
title: "ML_note #CNN-1(미완성)"
date: 2017-12-22
excerpt: "Machine Learning"
tags:
- Deep Learning
ref:
- 김성훈 교수님의 온라인 강의 및 논문
- 밑바닥부터 시작하는 딥러닝
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
- softmax
  - 각각의 output에 대해서 softmax함수 적용

**TIP**<br>
입력데이터의 채널 = 필터 채널<br>
filter의 개수 = 출력데이터의 채널<br>
{: .notice}

#### 학습 (BackProp)
