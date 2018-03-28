---
layout: post
title: "ML_note #6 딥러닝의 활용"
date: 2017-12-22
excerpt: "Machine Learning"
tags:
- Deep Learning
refs:
- 밑바닥부터 시작하는 딥러닝
comments: true
---
# 딥러닝의 활용

#### 사물검출
- R-CNN
- 이미지의 변형 및 분류에 SVM을 이용
- Selective Search 기법을 사용
- 후보 영역 추출까지 CNN으로 처리하는 Faster R-CNN기법도 등장

#### 분할
- 이미지 분류를 픽셀 수준에 적용
- FCN(Fully Convolutional Network)를 이용
- 합성곱 계층만으로 구성된 네트워크
- FCN의 마지막에 수행하는 확대는 이중 선형 보간에 의한 선형 확대

**NOTE**_완전 연결 계층에서는 출력이 모든 입력과 연결됩니다. 이와 같은 구성을 합성곱 계층으로도 구현할 수 있습니다. 가령 입력 크기가 32 * 10 * 10(채널32개, 높이 10, 너비 10)인 데이터에 대한 완전연결 계층은 필터 크기가 32 * 10 * 10인 합성곱 게층으로 대체할 수 있습니다. 만약, 완전연결 계층의 출력 노드가 100개라면 합성곱 계층에서는 기존의 32 * 10 * 10필터를 100개 준비하면 완전히 같은 처리를 할 수 있습니다. 이처럼 완전연결 계층은 같은 일을 수행하는 합성곱 계층으로 대체할 수 있습니다.
{: .notice}

#### 사진 캡션 생성
- NIC(Neural Image Caption)모델이 대표적
- CNN과 RNN의 조합으로 구성
- 사진이나 자연어와 같은 여러 정보를 조합 처리하는 것을 멀티모달 처리라고 함

#### 이미지 스타일(화풍) 변환
- <A Neural Algorithm of Artistic Style> 논문

#### 이미지 생성
- DCGAN(Deep Convolutional Generative Adversarial Network) 기법

**GAN**<br>
...
{: .notice}

#### 자율 주행
- SegNet이라는 CNN 기반 신경망
