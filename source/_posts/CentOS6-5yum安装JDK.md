---
title: '''CentOS6.5yum安装JDK'''
date: 2017-11-29 14:25:52
tags:
---
### 卸载之前版本的jdk
先查看 rpm -qa | grep java
显示如下信息：

java-1.4.2-gcj-compat-1.4.2.0-40jpp.115
java-1.6.0-openjdk-1.6.0.0-1.7.b09.el5
卸载：

rpm -e --nodeps java-1.4.2-gcj-compat-1.4.2.0-40jpp.115
rpm -e --nodeps java-1.6.0-openjdk-1.6.0.0-1.7.b09.el5

还有一些其他的命令

rpm -qa | grep gcj
rpm -qa | grep jdk

如果出现找不到openjdk source的话，那么还可以这样卸载

yum -y remove java java-1.4.2-gcj-compat-1.4.2.0-40jpp.115
yum -y remove java java-1.6.0-openjdk-1.6.0.0-1.7.b09.el5

### 确认卸载干净，开始安装

首先，在你的服务器上运行一下更新。

yum update

输入以下命令，查看已安装的JAVA版本

java -version

如果命令执行成功说明java还没有卸载完全，请回到第一步

yum search jdk
找到之后安装想要的版本
yum install java-xxx-openjdk.x86_64
等待下载完，java -verison测试一下即可
