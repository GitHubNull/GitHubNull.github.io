---
layout: post
title: "kali-linux-note"
date: 2017-10-17 11:56:10
image: 'kali-Linux-Destop.jpg'
description: 关于学习kali-Linux的笔记
category: '计算机'
tags:
- 计算机技术
twitter_text: 关于学习kali-Linux的笔记
introduction: 关于学习kali-Linux的笔记
color: '4A3341'
author: 夜雨
---

### Systemd

Systemd是一种新的linux系统服务管理器。它替换了init系统，能够管理系统的启动过程和一些系统服务，一旦启动起来，就将监管整个系统。

- 切换至字符界面
  ```sudo systemctl set-default multi-user.target```
- 切换至图形界面
  ```sudo systemctlset-default graphical.target```
- 打开图形界面
  ```sudo init 5```
