---
layout: post
title: "numpy"
date: 2018-03-05
excerpt: ""
tags:
- Python Note
comments: true
---
# Numpy

#### 개요
- 행렬 계산을 편리하게 해주는 파이썬 라이브러리

#### 기본
<pre><code>
  import numpy as np

  # 배열 생성
  arr = np.array([1,2,3])

  # 브로드캐스트
  arr = np.array([[1,2],[3,4]]) * np.array([1,2]) # [[1,4],[3,8]]

  # 원소 접근
  arr[1,1] # arr[1][1]
  arr[:] # 전체 행렬
  arr[:1] # 0번째 행까지
  arr[1:] # 1번째 행부터
</code></pre>
