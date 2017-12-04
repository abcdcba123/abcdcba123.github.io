---
title: 解决centos安装完java只能使用javac命令not found
date: 2017-12-04 21:56:12
tags:
---

### 在centos上yum安装完java，发现只能使用java命令，不能使用javac命令

网上查了一下，记录下步骤

首先更新一下yum咯

yum update

yum查找一下yum search java-1.8

看到了java-1.8.0-openjdk-devel.x86_64这个吗，安装它就可以了

yum -y install java-1.8.0-openjdk-devel.x86_64

ok，解决完毕