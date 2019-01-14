---
layout: post
title: "AWS/EC2 Django deploy"
date: 2018-07-12
excerpt: ""
tags:
- AWS
comments: true
---
#### AWS 서버세팅
... 이전글 참조

#### 과정
https://lhy.kr/ec2-ubuntu-deploy

#### 트러블 이슈...
- z-shell은 선택
- PATH설정은 다른글 참조...
- mysqlclient 설치오류
    # Command "python setup.py egg_info" failed with error code 1 in /tmp/pip-install-qh4xyb0p/mysqlclient/
    sudo apt-get install libmysqlclient-dev

- uWSGI작동확인
    uwsgi \
    --http :(port) \
    --home (virtualenv경로) \
    --chdir <django프로젝트 경로> \
    -w <설정 패키지명>.wsgi
    <설정 패키지명> -> 장고 프로젝트 안의 wsgi파일 위치

    /home/ubuntu/.pyenv/versions/uwsgi-env/bin/uwsgi \
    --http :8080 \
    --home /home/ubuntu/.pyenv/versions/django-deploy \
    --chdir /home/ubuntu/django \
    -w server.wsgi
    

- Nginx 서비스 파일 안만들면 작동 안함
    (uwsgi.service는 과정안에 들어가 있음)
    # /etc/systemd/system/Nginx.service
    [Unit]
    Description=The NGINX HTTP and reverse proxy server
    After=syslog.target network.target remote-fs.target nss-lookup.target

    [Service]
    Type=forking
    PIDFile=/run/nginx.pid
    ExecStartPre=/usr/sbin/nginx -t
    ExecStart=/usr/sbin/nginx
    ExecReload=/usr/sbin/nginx -s reload
    ExecStop=/bin/kill -s QUIT $MAINPID
    PrivateTmp=true

    [Install]
    WantedBy=multi-user.target

- Nginx 가상서버 설정 파일 작성
    uwsgi_pass = unix:///tmp/server.sock
    => tmp 파일에 넣으면 읽지를 못함
    => run 파일로 변경(이 두가지 파일 전부)
    /etc/nginx/sites-available/server.conf
    /프로젝트 디렉토리.../uwsgi.ini

#### Django Logging (EC2)
    # settings.py
    # LOG_DIR 는 접근이 가능해야 하므로 chmod나 chown 설정 변경해줘야 됨

    LOG_DIR = '/var/log'
    LOGGING = {
        'version': 1,
        'disable_existing_loggers': False,
        'filters': {
            'require_debug_false': {
                '()': 'django.utils.log.RequireDebugFalse',
            },
            'require_debug_true': {
                '()': 'django.utils.log.RequireDebugTrue',
            },
        },
        'formatters': {
            'django.server': {
                'format': '[%(asctime)s] %(message)s',
            }
        },
        'handlers': {
            'console': {
                'level': 'INFO',
                'filters': ['require_debug_true'],
                'class': 'logging.StreamHandler',
            },
            'file_error': {
                'class': 'logging.handlers.RotatingFileHandler',
                'level': 'ERROR',
                'formatter': 'django.server',
                'backupCount': 10,
                'filename': os.path.join(LOG_DIR, 'django_error.log'),
                'maxBytes': 10485760,
            }
        },
        'loggers': {
            'django': {
                'handlers': ['console', 'file_error'],
                'level': 'INFO',
                'propagate': True,
            },
        }
    }


    # views.py
    # 기본적인 로그가 찍히기는 하나...
    # Exception으로 처리해줌
    import logging

    logger = logging.getLogger("django")
  	try:
  		...
  	except Exception as e:
  		logger.error(e)
  		...
