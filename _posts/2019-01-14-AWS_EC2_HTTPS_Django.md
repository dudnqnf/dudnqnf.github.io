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

3. Django 프로젝트를 만들 디렉토리로 이동해서 stunnel을 위한 데이터들을 저장한 디렉토리를 만든다.

    $ mkdir stunnel
    $ cd stunnel





4. openSSL을 이용하여 SSL 통신을 위해 사용할 로컬 인증서와 키를 만든다.



$ openssl genrsa 1024 > stunnel.key

$ openssl req -new -x509 -nodes -sha1 -days 365 -key stunnel.key > stunnel.cert

$ cat stunnel.key stunnel.cert > stunnel.pem





5. 해당 인증서와 키를 사용하기 위해 config 파일을 만든다.



$ vim dev_https.conf



파일 내용은 아래와 같다.



[https]

accept=8443

connect=8001


TIMEOUTclose=1

cert = stunnel/stunnel.pem -> 본인환경에서 아까 생성한 stunnel.pem 의 절대경로를 입력한다.



이렇게 작성을 하면 stunnel은 포트 8443에서 수신을 대기하도록 하고, SSL에서 수신 한 모든 연결을 8001로 전달한다.







6. Django 프로젝트가 있는 디렉토리로 돌아가서 https를 실행시킬 수 있는 스크립트를 만든다.



$ cd ..

$ vim runserver



파일 내용은 아래와 같다.



stunnel stunnel/dev_https &

python 장고프로젝트명/manage.py runserver &


HTTPS=1 python 장고프로젝트명/manage.py runserver 8001



저장 후 실행을 가능하게 만들어준다.



$ chmod a+x runserver





7. 실행을 해본다.



$ ./runserver



https://localhost:8443 으로 접속을 하면 https 접속이 가능한 걸 확인할 수 있다! 겨우 성공했는데 내가 필요한 방법은 이 방법이 아니었고, 더 쉬운 방법도 있었다. 그 쉬운 방법을 해보고는 너무 허무했었는데 잘 기억이 안 나서 기억날 때 다시 추가해서 쓰도록 해야겠다.
