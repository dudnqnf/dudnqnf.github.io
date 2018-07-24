---
layout: post
title: "Ubuntu_pyenv"
date: 2018-07-02
excerpt: ""
tags:
- Python Note
comments: true
---
#### pyenv
    sudo apt-get install -y make build-essential libssl-dev zlib1g-dev libbz2-dev \
    libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev \
    xz-utils tk-dev

    curl -L https://raw.githubusercontent.com/yyuu/pyenv-installer/master/bin/pyenv-installer | bash

    # path 설정
    vi ~/.bashrc
    export PATH = $PATH:/home:/var
    export PATH="/root/.pyenv/bin:$PATH"
    eval "$(pyenv init -)"
    eval "$(pyenv virtualenv-init -)"
    source ~/.bashrc

    # pyenv 가상환경 만들기
    pyenv install --list
    pyenv install 3.6.4
    pyenv global 3.6.4
    pyenv versions

    # pyenv 가상환경 적용
    pyenv virtualenv 3.6.4 sample-env
    pyenv local sample-env
    pyenv shell uwsgi-env
