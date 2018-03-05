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
- 파이썬 라이브러리

#### 기본
<pre><code>
  import matplotlib.pyplot as plt

  # 데이터 준비
  x = np.arange(0, 6, 0.1)
  y = np.sin(x)

  # 그래프 그리기
  plt.plot(x, y)
  plt.show()

</code></pre>
