---
layout: post
title: "AWS/EC2 HTTPS Django"
date: 2019-01-14
excerpt: ""
tags:
- AWS
ref:
- http://kswims.tistory.com/121
- https://uwsgi-docs.readthedocs.io/en/latest/tutorials/Django_and_nginx.html
comments: true
---

0. AWS_EC2_Django 포스트 세팅
1. 추가 개념
- web client <-> the web server <-> the socket <-> uwsgi <-> Django

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

7. Service emperor로 변경
- /etc/systemd/system/uwsgi.service
        [Unit]
        Description=uWSGI Emperor service
        After=syslog.target

        [Service]
        User=ubuntu
        ExecStart=/home/ubuntu/.pyenv/versions/uwsgi-env/bin/uwsgi --emperor /home/ubuntu/django/.config/uwsgi/server.ini
        RuntimeDirectory=uwsgi
        Restart=always
        KillSignal=SIGQUIT
        Type=notify
        StandardError=syslog
        NotifyAccess=all
        StandardError=syslog

        [Install]
        WantedBy=multi-user.target

8. nginx 설정변경
- /etc/nginx/site-enable/server.conf
        upstream django {
        # server unix:///tmp/server.sock
        server 127.0.0.1;
        }

        server {
          listen 80;
          server_name *.compute.amazonaws.com; #*
          charset utf-8;
          client_max_body_size 128M;

          location / {
          uwsgi_pass  unix:///tmp/server.sock;
          include     uwsgi_params;
          }
        }

        server {
          listen       443;
          server_name  18.217.49.155;
          root         html;
          charset utf-8;
          client_max_body_size 128M;

          ssl                  on;
          ssl_certificate      /home/ubuntu/django/.config/uwsgi/stunnel.cert;
          ssl_certificate_key  /home/ubuntu/django/.config/uwsgi/stunnel.key;
          ssl_session_timeout  5m;
          ssl_protocols  SSLv2 SSLv3 TLSv1;
          ssl_ciphers  HIGH:!aNULL:!MD5;
          ssl_prefer_server_ciphers   on;

          location / {
            uwsgi_pass  unix:///tmp/server.sock;
            include     uwsgi_params;
          }
        }


9. https 속성 추가
- /프로젝트경로/.config/uwsgi/server.ini
        [uwsgi]
        chdir = /home/ubuntu/django
        module = server.wsgi:application
        home = /home/ubuntu/.pyenv/versions/django-deploy

        uid = ubuntu
        gid = ubuntu

        socket = /tmp/server.sock
        chmod-socket = 777
        chown-socket = ubuntu:ubuntu

        enable-threads = true
        master = true
        vacuum = true
        pidfile = /tmp/server.pid
        logto = /var/log/uwsgi/server/@(exec://date +%%Y-%%m-%%d).log
        log-reopen = true

        https = 0.0.0.0,/home/ubuntu/django/.config/uwsgi/stunnel.cert,/home/ubuntu/django/.config/uwsgi/stunnel.key,HIGH
