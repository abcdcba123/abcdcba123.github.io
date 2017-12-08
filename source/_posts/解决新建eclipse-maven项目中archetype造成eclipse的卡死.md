---
title: 解决新建eclipse maven项目中archetype造成eclipse的卡死
date: 2017-12-08 15:01:19
tags:
---
### 原因：eclipse maven每次都从http://repo1.maven.org/maven2/archetype-catalog.xml中下载文件，而这个文件比较大。


### 解决办法：自己下载下来，放在本地 并配置成eclipse在new maven项目时默认从本地下载。

#### 1.下载http://repo1.maven.org/maven2/archetype-catalog.xml这个文件，建议不要全选复制（太大有可能未加载完成就复制了），chrome中可右击另存为

#### 2. 在eclipse点击windows->preferences->Maven下拉三角形->archetypes有边框有archetypes的配置。选择添加本地的xml配置文件，Add Local Catalogs->File Location选择第一步创建的archtype-catalogs.xml,然后点击Apply->OK。
如图：
![](/images/解决新建eclipse-maven项目中archetype造成eclipse的卡死/2.png)

#### 3.重启eclipse,再次创建我的maven web项目，如果catalog的默认选项不是Default Local,记得要选择这个选项，再重启eclipse,发现这次不去网上找这个配置文件了，提供选择的catalogs的选择有一大堆，还可以filter过滤想要的模板,而且内存也在正常的200多兆。

如图：
![](/images/解决新建eclipse-maven项目中archetype造成eclipse的卡死/3.png)
