---
layout: post
title: "ML_note #2 Basic Model"
date: 2017-12-22
excerpt: "Machine Learning"
tags:
- Deep Learning
ref:
- 밑바닥부터 시작하는 딥러닝
comments: true
---
# 인공신경망
## 개요
- 데이터들이 어떤 선형그래프(y = Wx+b)를 그려내는지 추론하는 문제로 가정
- x(입력)에 대한 y(정답)을 주어주고 가중치(W)와 편향값(b)를 조정하는 모델

## 직관적 추론
- 학습
  - 수학시험에 50점(x)을 받으면 학점 2점(y) 이다
  - 수학시험에 70점(x)을 받으면 학점 3점(y) 이다
  - 수학시험에 90점(x)을 받으면 학점 4점(y) 이다
- 그래프 추론
  - W = 0.05, b = -0.5
  - y = 0.05 * x - 0.5
- 예측
  - 만약 80점을 맞으면 내 학점은 어떻게 될 것인가? 3.5점

## 인공신경망의 추론
- [ 예측 -> 학습(W와 b의 조정) ] 반복
- W : 1-> 0.5 -> 0.1 -> ... -> 0.05
- b : 1-> 0.3 -> 0 -> ... -> -0.5

---
## 퍼셉트론(신경망)
- 인간의 신경망을 모사
- y = wx + b
- x = 자극 / w = 민감도 / b = 역치 / y = 반응

## 활성화함수
자극에 대한 반응을 활성화 시키기 위한 함수<br>
추후 학습을 위해서 필요

#### 계단함수
$$h(x) =\begin{cases} 0\ (x\le0) \\ 1\ (x\gt0) \end{cases}$$

#### sigmoid
$$h(x) = \frac{1}{1+e^{-x}}$$

#### relu
$$h(x) =\begin{cases} 0\ (x\le0) \\ x\ (x\gt0) \end{cases}$$

---

## 출력함수
마지막 출력되는 값의 형태를 결정해 주는 함수

#### 항등함수
입력과 출력이 같은 함수<br>
$\sigma(x) = x$

#### softmax
각 입력값의 확률을 계산하는 함수<br>
$\sigma(x) = \frac{e^{x}}{\sum_{i=1}^n e^{i}}$

---

## Forward Propagation(예측)

#### Linear Regression
y = Wx + b

#### Logistic Classification
y = sigmoid(Wx+b)

#### Multinomial Logistic Regression
y = softmax(Wx+b)

#### Deep Neural Network
$y_1 = h_1(Wx+b)$ <br>
$y_2 = h_2(y_1)$ <br>
...<br>
$y_n = h_n(y_{n-1})$

---

## 손실함수
현재 학습한 모델의 정확도를 측정가능<br>
학습을 위한 지표
y = 출력, t = 정답

#### 평균 제곱 오차
$$E = \frac12 \sum_k(y-t)$$

#### Convex 오차
$$E = \begin{cases} -log(y)\ (if\ \ t = 1) \\ -log(1 - y)\ (if\ \ t = 0) \end{cases}$$
$$ = -tlog(y) - (1-t)log(1-y)$$

#### 교차 엔트로피 오차
$$E = -\sum_kt\ log(y)$$

---

## Back Propagation(학습)

#### 편미분 계산
- $y = x_1 + x_2$ 일때 $\frac{dy}{dx_1} = 1,\ \frac{dy}{dx_2} = 1$
- $y = x_1 * x_2$ 일때 $\frac{dy}{dx_1} = x_2,\ \frac{dy}{dx_2} = x_1$

#### 미분 연쇄
- $\frac{dz}{dx} = \frac{dz}{dy} * \frac{dy}{dx}$

#### Affine transformation(행렬 내적) 미분
- Y = WX 일때 $\frac{dY}{dX}=W^T, \frac{dY}{dW} = X^T$

#### 행렬 내적 미분 연쇄
- $\frac{dL}{dX} = \frac{dL}{dY} * \frac{dY}{dX} = \frac{dL}{dY} * W^T$
- $\frac{dL}{dW} = \frac{dY}{dW} * \frac{dL}{dY} = X^T * \frac{dL}{dY}$

#### Regression
- 층마다 활성화함수 포함
- 출력함수 : 항등함수
- 손실함수 : 평균 제곱 오차
- 출력함수 + 손실함수 미분값 : y-t

#### Classification
- 층마다 활성화함수 포함
- 출력함수 : softmax
- 손실함수 : 교차 엔트로피 오차
- 출력함수 + 손실함수 미분값 : y-t
