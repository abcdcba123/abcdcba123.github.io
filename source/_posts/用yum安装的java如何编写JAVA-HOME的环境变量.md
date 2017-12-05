---
layout: past
title: 用yum安装的java如何编写JAVA_HOME的环境变量
date: 2017-12-05 10:05:20
tags:
---

### yum安装完成java之后，查看jdk路径
which java
显示：/usr/bin/java
查看/usr/bin/java此地址对应的软连接（相当于一个快捷方式，我们需要找到快捷方式背后的真实文件）
ls -l /usr/bin/java
显示：lrwxrwxrwx. 1 root root 22 Aug 17 15:12 /usr/bin/java -> /etc/alternatives/java
继续寻找/etc/alternatives/java对应的真实文件
ls -l /etc/alternatives/java
显示：lrwxrwxrwx 1 root root 46 Nov 29 14:13 /etc/alternatives/java -> /usr/lib/jvm/jre-1.8.0-openjdk.x86_64/bin/java
现在找到了java对应的文件夹在/usr/lib/jvm/jre-1.8.0-openjdk.x86_64/bin/java

接下来开始真正的配置java的环境变量

vim /etc/profile.d/java_home.sh（ps:如果没有此文件，vim会自动创建，不用担心）

export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk.x86_64
export CLASSPATH=.:$JAVA_HOME/jre/lib/rt.jar:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
export PATH=$PATH:$JAVA_HOME/bin

设置好jdk的路径之后，需要运行下面的命令
source /etc/profile.d/java_home.sh
使得上面设置的环境变量立即生效。