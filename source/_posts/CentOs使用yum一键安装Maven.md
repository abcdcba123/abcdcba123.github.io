---
title: '''CentOs使用yum一键安装Maven'''
date: 2017-11-29 14:29:10
tags:
---

### 首先下载一下maven的repository
wget http://repos.fedorapeople.org/repos/dchen/apache-maven/epel-apache-maven.repo -O /etc/yum.repos.d/epel-apache-maven.repo
（这条命令表示：下载http://repos.fedorapeople.org/repos/dchen/apache-maven/epel-apache-maven.repo到服务器上的这个地址：/etc/yum.repos.d/epel-apache-maven.repo）
### yum安装
yum -y install apache-maven