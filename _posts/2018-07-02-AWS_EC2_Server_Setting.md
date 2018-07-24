---
layout: post
title: "AWS/EC2 Server Setting"
date: 2018-07-02
excerpt: ""
tags:
- AWS
comments: true
---
#### AWS 가입
#### EC2 인스턴스 생성
- Ubuntu Server 14.04 LTS (HVM)

#### putty/puttygen/pageant 설치
- https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html

#### puttygen/pageant
- public_key / private_key 생성
- EC2 키페어에 public_key 등록
- pageant : private_key 등록

#### putty
- public DNS or public IP
- connection -> SSH -> Auth 에서 private_key 등록(pageant 있으면 안해도 되는듯 함)
- 접속
- user_id : ubuntu

#### mysql
    # mysql 설치
    apt-get update
    apt-get install mysql-server

    # mysql 접속
    select host, user, password from user;
    GRANT ALL PRIVILEGES ON *.* TO '계정명'@'%';
    FLUSH PRIVILEGES;

    # mysql 외부접속 설정변경
    vim /etc/mysql/my.cnf
    bind-address = 0.0.0.0
    service mysqld restart

- EC2 인바운드 규칙 변경


#### pyenv 설치
    sudo apt-get install -y make build-essential libssl-dev zlib1g-dev libbz2-dev \
    libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev \
    xz-utils tk-dev

    curl -L https://raw.githubusercontent.com/yyuu/pyenv-installer/master/bin/pyenv-installer | bash

    # path설정
    vi ~/.bashrc
    export PATH = $PATH:/home:/var
    export PATH="/root/.pyenv/bin:$PATH"
    eval "$(pyenv init -)"
    eval "$(pyenv virtualenv-init -)"
    source ~/.bashrc

    pyenv
