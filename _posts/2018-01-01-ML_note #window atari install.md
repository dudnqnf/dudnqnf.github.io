---
layout: post
title: "윈도우에서 아타리 설치방법"
date: 2018-01-01
excerpt: "Machine Learning"
tags:
- Reinforcement Learning
comments: true
---

# 윈도우에서 아타리 설치방법

#### MSYS2
- http://www.msys2.org/
- CMAKE 등 설치를 위해 필요
- msys2실행
  - <code>pacman -S base-devel mingw-w64-x86_64-gcc mingw-w64-x86_64-cmake</code>

#### 시스템 환경변수 변경
- DISPLAY = :0  (새로만들기)
- PHTYONPATH = c:\path\to\atari-py:$PYTHONPATH  (새로만들기)
- path
  - C:\msys64\mingw64\bin (추가)
  - C:\msys64\usr\bin (추가)

#### Xming X server 설치
- https://sourceforge.net/projects/xming/?source=directory
- linux게임을 GUI로 표현할 때 사용되는듯...

#### atari 설치
- git 설치
- cmd 실행
  - <code>git clone https://github.com/rybskej/atari-py</code>
  - <code>cd atari-py</code>
  - <code>make</code>
  - <code>python setup.py install</code>
  - <code>pip install -U git+https://github.com/Kojoley/atari-py.git</code>

#### 오류수정
- pip install gym[atari]로 하면 오류남

---
> 출처 : http://ishuca.tistory.com/entry/Windows에서-gymatari-설치하기
