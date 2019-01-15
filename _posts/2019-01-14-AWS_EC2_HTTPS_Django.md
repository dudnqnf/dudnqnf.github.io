---
layout: post
title: "AWS/EC2 HTTPS Django"
date: 2019-01-14
excerpt: ""
tags:
- AWS
ref:
- http://kswims.tistory.com/121
comments: true
---

1. openSSL 설치 (https://www.openssl.org)
        $ wget https://www.openssl.org/source/openssl-1.1.0e.tar.gz
        $ tar xvfz openssl-1.1.0e
        $ cd openssl-1.1.0e
        $ ./config
        $ make
        $ make test
        $ make install

2. stunnel 설치 (https://www.stunnel.org/)
        $ wget https://www.stunnel.org/downloads/stunnel-5.48.tar.gz
        $ tar xvfz stunnel-5.48
        $ cd stunnel-5.48
        $ ./configure
        $ make
        $ make test
        $ make install

4. openSSL을 이용하여 로컬 인증서와 키 생성
        $ openssl genrsa 1024 > stunnel.key
        $ openssl req -new -x509 -nodes -sha1 -days 365 -key stunnel.key > stunnel.cert
        $ cat stunnel.key stunnel.cert > stunnel.pem

5. EC2 HTTPS 인바운드 수정

6. UWSGI 테스트
        /home/ubuntu/.pyenv/versions/uwsgi-env/bin/uwsgi \
        --https :443,stunnel.cert,stunnel.key,HIGH \
        --home /home/ubuntu/.pyenv/versions/django-deploy \
        --chdir /home/ubuntu/django \
        -w server.wsgi
