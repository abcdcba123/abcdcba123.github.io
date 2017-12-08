---
title: eclipse无法导入java项目
date: 2017-12-08 10:31:24
tags:
---

### 原因一：java项目缺少.project和.classpath文件

解决办法：去别的java项目中吧.project和.classpath文件拷贝过来，并且把.project中的name标签中的名称改一下，不要与别的相同

### 原因二：.project文件中的name标签中的名称与别的项目重复了！

解决办法：把.project中的name标签中的名称改一下，不要与别的相同