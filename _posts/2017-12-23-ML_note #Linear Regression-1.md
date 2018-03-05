---
layout: post
title: "ML_note #Linear Regression-1(미완성)"
date: 2017-12-22
excerpt: "Machine Learning"
tags:
- Deep Learning
comments: true
---
# Linear Regression(선형회귀)
#### 개요
- 교사학습의 가장 기본적인 모델
- 문제와 정답을 통해서 학습
- 어떤 선형그래프를 그려내는지 추론하는 것(y = ax+b)
- x(입력)에 대한 y(정답)을 주어주고 가중치(a)와 bias(b)를 추론하는 것

#### 기본문제
- 학습
  - 수학시험에 50점(입력)을 받으면 C(정답) 였다
  - 수학시험에 70점(입력)을 받으면 B(정답) 였다
  - 수학시험에 90점(입력)을 받으면 A(정답) 였다
- 학습을 통해 근사되어갈 그래프
  - A = 4, B = 3, C = 2 이라고 할 떄( (+)점수는 0.5 )
  - y = 0.05 * x - 0.5 (a = 0.05, b = -0.5)로 근사될 것
- 예측
  - 만약 80점을 맞으면 내 학점은 어떻게 될 것인가? B+(정답)

#### 학습은 어떻게?
- Cost
- Regression


#### 모델
- 정식표기 : Y = WX + b

#### sigmoid
#### relu
#### softmax
