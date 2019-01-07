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
    https://sites.google.com/a/chromium.org/chromedriver/

- Set path
    # hash shell
    vim ~/.bashrc
    # zshell
    vim ~/.zshrc

    export path="$PATH:경로"

- Install
    sudo apt-get -y install google-chrome-stable
    sudo apt-get install libnss3-dev

#### Trouble Issue
- Use Python Loggin
- (beautifulsoup4) html5lib -> lxml
