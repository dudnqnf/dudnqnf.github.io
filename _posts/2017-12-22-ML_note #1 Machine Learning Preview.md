---
layout: post
title: "ML_note #1 Machine Learning Preview"
date: 2017-12-22
excerpt: "Machine Learning"
tags:
- Deep Learning
comments: true
---
# Machine Learning Preview
## 교사학습(Superviced Learning)
- 각각의 입력에 대한 정답값이 존재할 때 이용가능한 알고리즘
- Linear regression(선형회귀)
    - 다항식으로 표현 가능한 상관관계(함수)
- Neural Network
  - DNN(Deep Neural Network)
    - 다항식으로 표현 불가능한 상관관계도 포함
  - CNN(Convolutional Neural Network)
    - 그림 인식 (개와 고양이 그림 분류)
  - RNN(Recurrent Neural Network)
    - 앞의 내용을 통한 다음 문자 부분 예측
    - 앞의 파동을 통한 다음 파동(시계열) 부분 예측

## 비교사학습(Unsuperviced Learning)
- 입력에 대한 정답이 없고 문제들간의 공통점 추출할 때 이용가능한 알고리즘
- Clustering(군집화)에 주로 사용
- SOM, Hopfield ...

## 강화학습(Reinforcement Learning)
- 각각 입력값들에 대한 정답이 아닌 전체에 대한 평가값만 존재할 때 이용가능한 알고리즘
- TSP문제(헤밀턴 경로 탐색) 등 NP문제
- 알파고(몬테카를로)
- DQN, A3C ...

## 이 외
- SVM, RandomForest, ...
