---
title: phpstorm打开后一直停留在scanning files to index....或跳出内存不够的提示框
date: 2017-12-06 11:34:32
tags:
---

### 说明
在npm install 后，会出现Scanning files to index ...... 出现这个是正常的，但是一直不消失就不正常了。

原因是npm install 后 node_modules 内增加了文件夹，但是文件路劲太深所以 才造成phpstorm 一直卡在了 Scanning files to index.... 状态。之后会出现提示框，也就是提示说给phpstorm分配的内存太少。但是，自己要知道，并不是分配的内存少哦。


### 解决办法

右击 node_modules文件夹，在出现的框中选择Mark Directory As，再选择Excluded

也就是让phpstorm不加载这个文件夹。
如图：
![](/images/phpstorm打开后一直停留在scanning-files-to-index-或跳出内存不够的提示框/1.png)

转载自：http://blog.csdn.net/qq_31411389/article/details/54291243
