---
layout: post
title: "AWS/EC2 Selenium"
date: 2018-07-16
excerpt: ""
tags:
- AWS
comments: true
---

#### Process
- Download webdriver
    http://chromedriver.storage.googleapis.com/index.html

- Set path
    # hash shell
    vim ~/.bashrc
    # zshell
    vim ~/.zshrc

    export path="$PATH:경로"
    source ~/.shell_name

- Install
    sudo apt-get -y install google-chrome-stable
    sudo apt-get install libnss3-dev

#### Django
- (beautifulsoup4) html5lib -> lxml

#### Nodejs
- chrome-option (--no-sandbox) 추가
