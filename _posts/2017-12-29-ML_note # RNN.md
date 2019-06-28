---
layout: post
title: "ML_note #5 RNN(작성중)"
date: 2017-12-22
excerpt: "Machine Learning"
tags:
- Deep Learning
refs:
- https://deeplearning4j.org/kr/lstm
- https://github.com/WegraLee/deep-learning-from-scratch
comments: true
---
# Recurrent Neural Network(RNN)

#### 개요
- 출력값이 다시 입력으로 들어가는 형태의 DNN
- 시계열 예측, 문자 인식 기술에 좋은 성과를 보이고 있는 알고리즘

#### (Vanilla) RNN 구조
$h_t = φ(Wx_t + Uh_{t-1})$
- $x_t$ = 입력
- $W$ = 가중치
- $U$ = 전이계수
- $φ$ = 활성화함수(tanh, sigmoid)

#### LSTM(Long Short Term Memory Units)
- 현재 가장 널리 쓰이고 있는 RNN구조


#### 학습 (BackProp)
- BPTT(Backpropagation Through Time) : 시간을 거슬러 올라가며 backprop
