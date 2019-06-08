---
title: 2 认识html标签
date: 2019-03-06 16:50:18
tags: html入门
desc: 
# keywords: 
categories:
  - html入门
# from: https://bitsofco.de/the-background-properties/
# demo: ../../../demos/201703/background.html
---

<a name="10369f11"></a>
### 2.1 入门篇

<a name="cfb83c02"></a>
#### 世界观

     在张鑫旭大神将前端的世界比喻成一个王国，而我认为可能这就分为3个部队，差不多可以理解成为，html部队，css部队，js部队。有一个叫产品经理的怪，需要三家合理才能打赢。

    这第一仗就是html，负责把骨架搭好了，再上颜料和动态效果。骨架搭的好，有什么好处呢，大家都知道只要div+css，那么这个页面除了几个特殊标签，比如a，viode啊，其他的都可以伪装出来。这个牵扯到一个标签语义化的作用，语义化有两种好处。

<a name="9c983fd3"></a>
### 2.2 权重(蜘蛛)

     骨架好，百度蜘蛛会爬取收录。这个作用，可以帮助很多公司，获取百度权重的排名。百度蜘蛛，它的功能其实就和抄书一样。那么就意味着他不能解析css。所以，他看到了img就知道是图片，但是你写一个div+background:url('./img.png')。它可就不认识了。

<a name="adc00fab"></a>
### 2.3 障碍解析器

     使用特殊的阅读器。

> 那么如何判断骨架的好坏呢？


     我们拿慕课网举例子，原图如下

![](https://cdn.nlark.com/yuque/0/2019/png/271124/1551858682311-ba33b5ea-4aa3-45a7-9b40-2b9eb19b592b.png#align=left&display=inline&height=164&originHeight=423&originWidth=1919&size=0&status=done&width=746)

     我们把网页的css删除了，标签的格式还不乱，这就是好的骨架。

![](https://cdn.nlark.com/yuque/0/2019/png/271124/1551858682559-cca75bd2-0336-470a-a0c3-692ec42ad69d.png#align=left&display=inline&height=411&originHeight=411&originWidth=307&size=0&status=done&width=307)

改呗收录的都被收录了这就是语义化。

> 按下不表: 接下来我们将根据 html，css，js的基本和升级探究，前端的世界。


