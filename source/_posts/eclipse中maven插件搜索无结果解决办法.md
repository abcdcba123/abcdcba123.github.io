---
title: eclipse中maven插件搜索无结果解决办法
date: 2017-11-14 17:42:34
tags:
---

在maven中导入jar包可能会遇到各种问题

### 第一个问题：
eclipse中并不会出现正常的select界面，会提示：

{% codeblock lang:objc %}
[rectangle setX: 10 y: 10 width: 20 height: 20];
{% endcodeblock %}

{% codeblock %}
alert('Hello World!');
{% endcodeblock %}

{% codeblock Array.map %}
array.map(callback[, thisArg])
{% endcodeblock %}

![](/images/eclipse中maven插件搜索无结果解决办法/1.png)

可能的原因是：maven自动下载index组件的功能没有开启

解决办法：
点击："Window" -> "Preferences" 然后在左侧栏选择"maven"，勾选 Download repository index updates on startup
如图所示：
![](/images/eclipse中maven插件搜索无结果解决办法/2.png)

### 第二个问题：
eclipse中并不会出现正常的select界面，啥都不提示，就是无法搜索远程库
可能的原因是：没有配置可用的仓库或者仓库的索引损坏导致无法检索

解决办法：
首先打开eclipse中的Maven Repositories视图
![](/images/eclipse中maven插件搜索无结果解决办法/3.png)
![](/images/eclipse中maven插件搜索无结果解决办法/4.png)
![](/images/eclipse中maven插件搜索无结果解决办法/5.png)
在上图中的cental(http://repo1...)上右击之后，选择rebuild index(full index enabled如果没有选中也需要选中)



