---
layout: post
title: "AWS/EC2 HeidiSQL"
date: 2018-08-24
excerpt: ""
tags:
- AWS
comments: true
---

#### 설정 탭
- 네트워크 유형 : MYSQL (SSH tunnel)
- 호스트명 : EC2 서버주소
- 사용자 : MySql 아이디
- 암호 : MySql 비밀번호
- 포트 : 3306 (default)

#### SSH 터널 탭
- plink.exe 위치 : 다운로드 후 위치 설정
- SSH 호스트 + 포트 : EC2 서버주소 + 22 (default)
- 사용자 이름 : ubuntu
- 암호 : 공란
- 개인 키 파일 : private_key.pem 주소
- 로컬포트 : 3307 (default)
