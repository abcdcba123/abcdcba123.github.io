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


本人真实使用了一下，发现版本一直是3.3.9的，后来我还是到官网去下载了一份最新版的。
官网地址：http://maven.apache.org/
找到bin的文件下载
![](/images/CentOs使用yum一键安装Maven/4.jpg)
下载完了就上传到服务器的某个目录（ps:例如：/usr/local/src，下文请用自己的目录代替此目录）

进入此目录
cd /usr/local/src
把文件解压
如果下载的是tar.gz文件则执行：
tar xzvf apache-maven-XXXX-bin.tar.gz
如果下载的是zip文件则执行：
unzip apache-maven-XXXX-bin.zip
此时解压文件就在/usr/local/src下面（ps：如果想解压到别的文件夹，使用tar xzvf apache-maven-XXXX-bin.tar.gz -C 其他目录）

最后一步，配置环境变量
vim /etc/profile.d/maven.sh（ps:如果没有此文件，vim会自动创建，不用担心）
在vim界面中输入：
export MAVEN_HOME=/usr/local/src/apache-maven-bin（ps:此处是你解压的目录）
export PATH=${MAVEN_HOME}/bin:${PATH}

设置好Maven的路径之后，需要运行下面的命令
source /etc/profile.d/maven.sh
使得上面设置的环境变量立即生效。