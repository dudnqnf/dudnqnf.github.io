---
layout: post
title: "matplotlib"
date: 2018-03-05
excerpt: ""
tags:
- Python Note
comments: true
---
# matplotlib

#### 개요
- 그래프를 그려주는 파이썬 라이브러리

#### 기본
<pre><code>
  import matplotlib.pyplot as plt

  # 데이터 준비
  x = np.arange(0, 6, 0.1) # 0에서 6까지 0.1 간격으로 생성
  y1 = np.sin(x)
  y2 = np.cos(x)

  # 그래프 그리기
  plt.plot(x, y1, label="sin")
  plt.plot(x, y2, linestyle = "--", label="cos") # cos 함수는 점선으로 그리기
  plt.xlabel("x") # x축 이름
  plt.ylabel("y") # y축 이름
  plt.title('sin & cos')  # 제목
  plt.legend()
  plt.show()
</code></pre>

#### 이미지 표시
<pre><code>
  import matplotlib.pyplot as plt
  from matplotlib.image import imread

  img = imread('../dataset/lena.png') # 이미지 읽어오기
  plt.imshow(img)

  plt.show()
</code></pre>
