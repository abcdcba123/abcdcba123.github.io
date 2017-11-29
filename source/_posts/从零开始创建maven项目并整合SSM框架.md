---
title: 从零开始创建maven项目并整合SSM框架
date: 2017-11-17 13:51:28
tags:
---

### 第一步：搭建java环境以及下载好IDE（eclipse或者myeclipse）
  如果不会请参照教程：

### 第二步：在eclipse中新建一个maven项目
如图所示：
![](/images/从零开始创建maven项目并整合SSM框架/1.png)
![](/images/从零开始创建maven项目并整合SSM框架/2.png)
![](/images/从零开始创建maven项目并整合SSM框架/3.jpg)
![](/images/从零开始创建maven项目并整合SSM框架/4.jpg)
在上图中的：Group id和Artifact id需要全局唯一。这是初级教程，就不详细解释了，百度一下就知道了。一般package名为Group id 加上 Artifact id
这时候会看到一些错误，先不管它：
如图：
![](/images/从零开始创建maven项目并整合SSM框架/5.png)
### 第三步：设置jre为1.8或者适合的版本以及把Dynamic web module改为3.1或对应版本
首先：eclipse调整jre版本有三个地方需要调整
如图所示：
第一个地方修改：
点开properties找到如下：
![](/images/从零开始创建maven项目并整合SSM框架/6.jpg)
选中之后点edit:
![](/images/从零开始创建maven项目并整合SSM框架/7.jpg)
选择完成之后应该变成：
![](/images/从零开始创建maven项目并整合SSM框架/8.jpg)
到这里，第一个地方修改完毕。

第二个地方修改：
点开properties找到如下：
![](/images/从零开始创建maven项目并整合SSM框架/11.jpg)
修改完毕。

第三个地方修改：
![](/images/从零开始创建maven项目并整合SSM框架/9.jpg)
修改完jre版本之后，还需要在这里修改Dynamic web module版本。
这个时候碰到了问题，不让修改。这时候需要去.settings文件夹中修改文件。
首先找到项目中的.settings文件，比如我的地址是：D:\eclipse-workspace\ssmDemo\.settings
项目中为：
![](/images/从零开始创建maven项目并整合SSM框架/13.png)
用另外的编辑器打开三个文件，做如下修改：
![](/images/从零开始创建maven项目并整合SSM框架/12.png)
![](/images/从零开始创建maven项目并整合SSM框架/14.png)
![](/images/从零开始创建maven项目并整合SSM框架/15.png)
修改完成后回到eclipse，发现Dynamic web module已经变成了3.1
![](/images/从零开始创建maven项目并整合SSM框架/19.png)

### 第四步：使用maven导入必要的jar包

进入如下界面，并打开pom.xml（ps：请注意maven文件夹格式：src/main/java,src/main/resources,src/test/java这三个source folder必须要有，没有的话，就去文件夹中建立相应的文件夹）
![](/images/从零开始创建maven项目并整合SSM框架/20.png)
进行如下点击：
![](/images/从零开始创建maven项目并整合SSM框架/21.jpg)

进入到如下界面，发现一个问题，没有相应的索引，我们需要去给maven重新建立索引。
![](/images/从零开始创建maven项目并整合SSM框架/22.png)
参照我的另一篇文章：
{% blockquote https://abcdcba123.github.io/2017/11/14/eclipse中maven插件搜索无结果解决办法 %}
eclipse中maven插件搜索无结果解决办法
{% endblockquote %}

一步一步增加所需要的包
{% codeblock [我的pom.xml] [lang:xml] %}
my pom.xml codeblock
{% endcodeblock %}


### 第五步：建立起必要的包和文件夹
在src/main/java中建立如下所示的包：
![](/images/从零开始创建maven项目并整合SSM框架/24.png)
在src/main/resources中建立两个文件夹：
![](/images/从零开始创建maven项目并整合SSM框架/23.png)

| 文件名        | 作用  |
| :--------:   | :--------------: |
| src       |   根目录 |
| main        |  主要目录，可以放java代码和一些资源文件。    |
| java        |  存放我们的java代码，这个文件夹要使用Build Path -> Use as Source Folder，这样看包结构会方便很多，新建的包就相当于在这里新建文件夹咯。    |
| resources        |  存放资源文件，譬如各种的spring，mybatis，log配置文件。    |
| mapper        |  存放dao中每个方法对应的sql，在这里配置，无需写daoImpl。    |
| spring        |  这里当然是存放spring相关的配置文件，有dao service web三层。   |
| sql        |  其实这个可以没有，但是为了项目完整性还是加上吧。   |
| webapp        |  用来存放我们前端的静态资源，如jsp js css。   |
| WEB-INF        |  很重要的一个目录，外部浏览器无法访问，只有羡慕内部才能访问，可以把jsp放在这里，另外就是web.xml了。你可能有疑问了，为什么上面java中的resources里面的配置文件不妨在这里，那么是不是会被外部窃取到？你想太多了，部署时候基本上只有webapp里的会直接输出到根目录，其他都会放入WEB-INF里面，项目内部依然可以使用classpath:XXX来访问，好像IDE里可以设置部署输出目录，这里扯远了~    |
| test        |  这里是测试分支。    |
| java        |  测试java代码，应遵循包名相同的原则，这个文件夹同样要使用Build Path -> Use as Source Folder，这样看包结构会方便很多。   |
| resources        |  这里的资源是指项目的静态资源，如js css images等。    |
| resources        |  这里的资源是指项目的静态资源，如js css images等。    |

### 第六步：开始编码
#### 配置数据库连接(jdbc.properties)
{% codeblock [jdbc.properties] %}
jdbc.driver=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql://localhost:3306/ssm?useUnicode=true&characterEncoding=utf8
jdbc.username=root
jdbc.password=root
{% endcodeblock %}
#### 配置spring的dao层
{% codeblock [spring-dao.xml] [lang:xml] %}
my spring-dao.xml
{% endcodeblock %}

#### 配置mybatis
{% codeblock [mybatis-config.xml] [lang:xml] %}
my mybatis-config.xml
{% endcodeblock %}

#### 配置spring
{% codeblock [spring-dao.xml] [lang:xml] %}
my spring-dao.xml
{% endcodeblock %}
{% codeblock [spring-service.xml] [lang:xml] %}
my spring-service.xml
{% endcodeblock %}
{% codeblock [spring-controller.xml] [lang:xml] %}
my spring-controller.xml
{% endcodeblock %}

最后总结一下，带上pom.xml一共配置了8个文件，如图：
![](/images/从零开始创建maven项目并整合SSM框架/30.png)

#### 配置过程需要注意的地方（配置完成可以跳过）
![](/images/从零开始创建maven项目并整合SSM框架/31.png)
![](/images/从零开始创建maven项目并整合SSM框架/32.png)
![](/images/从零开始创建maven项目并整合SSM框架/33.png)
![](/images/从零开始创建maven项目并整合SSM框架/34.png)
![](/images/从零开始创建maven项目并整合SSM框架/35.png)
![](/images/从零开始创建maven项目并整合SSM框架/36.png)

到这里配置工作已经完成了，用引用的文章中的小项目检验
### 第七步：SSM框架应用实例（简单图书管理系统）
#### 建表，插入数据
首先新建数据库名为ssm，再创建两张表：图书表book和预约图书表appointment，并且为book表初始化一些数据，sql如下。
{% codeblock [schema.sql] [lang:sql] %}
-- 创建图书表
CREATE TABLE `book` (
  `book_id` bigint(20) NOT NULL AUTO_INCREMENT COMMENT '图书ID',
  `name` varchar(100) NOT NULL COMMENT '图书名称',
  `number` int(11) NOT NULL COMMENT '馆藏数量',
  PRIMARY KEY (`book_id`)
) ENGINE=InnoDB AUTO_INCREMENT=1000 DEFAULT CHARSET=utf8 COMMENT='图书表'

-- 初始化图书数据
INSERT INTO `book` (`book_id`, `name`, `number`)
VALUES
	(1000, 'Java程序设计', 10),
	(1001, '数据结构', 10),
	(1002, '设计模式', 10),
	(1003, '编译原理', 10)

-- 创建预约图书表
CREATE TABLE `appointment` (
  `book_id` bigint(20) NOT NULL COMMENT '图书ID',
  `student_id` bigint(20) NOT NULL COMMENT '学号',
  `appoint_time` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '预约时间' ,
  PRIMARY KEY (`book_id`, `student_id`),
  INDEX `idx_appoint_time` (`appoint_time`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='预约图书表'
{% endcodeblock %}

#### 在entity包中添加两个对应的实体，图书实体Book.java和预约图书实体Appointment.java。
{% codeblock [Book.java] [lang:java] %}
Book.java
{% endcodeblock %}

{% codeblock [Appointment.java] [lang:java] %}
Appointment.java
{% endcodeblock %}

#### 在dao包新建接口（注意：是接口interface）BookDao.java和Appointment.java

{% codeblock [BookDao.java] [lang:java] %}
BookDao.java
{% endcodeblock %}

{% codeblock [AppointmentDao.java] [lang:java] %}
AppointmentDao.java
{% endcodeblock %}

#### 编写mybatis需要的mapper文件（ps:不需要实现dao接口不用编写daoImpl， mybatis会给我们动态实现，但是我们需要编写相应的mapper）

{% codeblock [BookDao.xml] [lang:xml] %}
BookDao.xml
{% endcodeblock %}

{% codeblock [AppointmentDao.xml] [lang:xml] %}
AppointmentDao.xml
{% endcodeblock %}

#### 测试代码（这里就不阐述了，直接去下面的引用的文章中看）

#### 定义给客户端返回的信息
新建一个包叫enums，在里面新建一个枚举类AppointStateEnum.java，用来定义预约业务的数据字典。
{% codeblock [AppointStateEnum.java] [lang:java] %}
AppointStateEnum.java
{% endcodeblock %}

接下来，在dto包下新建AppointExecution.java用来存储我们执行预约操作的返回结果。

{% codeblock [AppointExecution.java] [lang:java] %}
AppointExecution.java
{% endcodeblock %}

接着，在exception包下新建三个文件 NoNumberException.java RepeatAppointException.java AppointException.java 预约业务异常类（都需要继承RuntimeException），分别是无库存异常、重复预约异常、预约未知错误异常，用于业务层非成功情况下的返回（即成功返回结果，失败抛出异常）。

{% codeblock [NoNumberException.java] [lang:java] %}
NoNumberException.java
{% endcodeblock %}
{% codeblock [RepeatAppointException.java] [lang:java] %}
RepeatAppointException.java
{% endcodeblock %}
{% codeblock [AppointException.java] [lang:java] %}
AppointException.java
{% endcodeblock %}

#### 开始编写业务代码

在service包下新建BookService.java图书业务接口（注意：是接口interface）
{% codeblock [BookService.java] [lang:java] %}
BookService.java
{% endcodeblock %}

在service.impl包下新建BookServiceImpl.java使用BookService接口，并实现里面的方法。
{% codeblock [BookServiceImpl.java] [lang:java] %}
BookServiceImpl.java
{% endcodeblock %}

在dto包里新建一个封装json返回结果的类Result.java，设计成泛型。
{% codeblock [Result.java] [lang:java] %}
Result.java
{% endcodeblock %}

我们写controller层，我们在controller包下新建BookController.java文件。
{% codeblock [BookController.java] [lang:java] %}
BookController.java
{% endcodeblock %}

#### 用postman测试


#### （核心）从网络访问到程序执行总结
从网络访问之后，程序进入controller层，接收到地址和参数
spring根据地址找到controller层的方法：
![](/images/从零开始创建maven项目并整合SSM框架/40.png)
通过注解BookController上面的注解@RequestMapping("/book")以及
appoint方法上面的注解@RequestMapping(value = "/{bookId}/appoint", method = RequestMethod.POST, produces = {
              			"application/json; charset=utf-8" })
确定这个方法的访问地址url是：/book/参数bookId/appoint。
然后访问方式是：POST
方法中获取到的参数是：
第一个：bookId（这个是通过url中的参数bookId获取，使用@PathVariable("bookId")获取）
第二个：studentId（这个是通过post提交的form表单获取，使用@RequestParam("studentId") 获取）
ps:这里获取参数有很多种方式，也有一些坑，我总结了一些个人碰到的，请参照我的另一篇文章
{% blockquote https://abcdcba123.github.io/2017/11/14/eclipse中maven插件搜索无结果解决办法 %}
spring获取get和post参数遇到的坑
{% endblockquote %}

拿到参数之后：
处理，并调用service层的方法处理数据，service层可以调用dao层进行数据库交互，这中间主要需要注意的是与数据库的交互，使用mybatis与数据库交互，是这样的：
首先要连接数据库：通过jdbc.properties配置数据库地址用户名啥的。
通过mybatis-config.xml配置mybatis（copy过来就行，没啥好说的，更细的内容需要自己读文档）
在spring-dao.xml中配置spring扫描的配置文件：
![](/images/从零开始创建maven项目并整合SSM框架/41.png)
![](/images/从零开始创建maven项目并整合SSM框架/42.png)
可以看到它扫描了jdbc.properties、mybatis-config.xml、entity包下所有文件、mapper下所有xml、dao包下所有文件
entity是实体类，用来定义查询完成之后的返回数据，其中的字段应该和数据库表的字段一样
dao包中是定义的数据库查询接口
mapper下的xml文件是定义实现dao接口的sql语句

让我们来看一个具体例子：
![](/images/从零开始创建maven项目并整合SSM框架/43.png)
进入到controller之后，第一个框框检测参数是否符合规定
第二个框调用了servic层中BookService接口定义的appoint方法，这个appoint方法的实现是在BookServiceImpl中
我们进入appoint方法：
![](/images/从零开始创建maven项目并整合SSM框架/44.png)
传入了bookId和studentId
使用bookId去BookDao层调用reduceNumber方法
进入reduceNumber方法（套路也是一样的，reduceNumber方法在BookDao接口定义，但是它的实现是通过src/main/resources/mapper/BookDao.xml中，中间使用了mybatis，过程不阐述了，先知道怎么使用）：
![](/images/从零开始创建maven项目并整合SSM框架/45.png)
其中reduceNumber方法传入了一个bookId，在xml中是使用#{bookId}获取，返回值是一个int，表示是否成功减少number。

其他的方法都类似，这就是访问数据库的全过程，最后如果正常预约会返回一个AppointExecution（请区别于Exception，Exception是异常，Execution是自己定义的一个返回客户端的类），预约失败返回异常（Exception）信息
最后回到controller层，根据返回结果和异常的不同，返回不同的AppointExecution
然后把AppointExecution放入到Result方法中，返回对应json数据







以上内容大部分来自git上liyifeng1994的ssm项目，转载自：
https://github.com/liyifeng1994/ssm
致敬！

