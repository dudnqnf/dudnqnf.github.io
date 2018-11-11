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

#### EC2
- 인바운드 설정
- 키 페어 설정

#### puttygen/pageant
- public_key / private_key 생성
- EC2 키페어에 public_key 등록
- pageant : private_key 등록

#### putty
- public DNS or public IP
- connection -> SSH -> Auth 에서 private_key 등록(pageant 있으면 안해도 되는듯 함)
- 접속
- user_id : ubuntu

#### Trouble shouting
- SSH 접속 불가
  - ERROR : no supported authentication methods available server sent publickey
  - private_key / public_key 를 미리 생성 후 인스턴스 만들때 넣어주기
  - 어떤 서버냐에 따라 Default 아이디 / SSH 접속 환경이 다를 수 있음
  - 다양한 서버 시도

#### mysql
    # mysql 설치
    apt-get update
    apt-get install mysql-server

    # mysql 접속
    mysql -u root -p
    use mysql;
    select host, user from user;
    create user '계정명'@'%' identified by '비밀번호';
    grant all privileges on *.* to '계정명'@'%';
    flush privileges;

    # mysql 외부접속 설정변경
    vim /etc/mysql/my.cnf
    bind-address = 0.0.0.0
    service mysqld restart

    # mysql 외부접속 설정변경2
    vim /etc/mysql/mysql.conf.d/mysqld.cnf
    bind-address = 0.0.0.0
    service mysql restart
