---
title: 4 优化html
date: 2019-04-15 15:10:04
tags: 前端优化方案
desc: 
# keywords: 
categories:
  - 前端优化方案
# from: https://bitsofco.de/the-background-properties/
# demo: ../../../demos/201703/background.html
---

<a name="1301f740"></a>
### 4.1 audio或者video标签
如果当页面中出现audio或者video标签，我们最好设置它们的preload=:页面加载的时候，音视频资源不进行加载，播放的时候再开始加载(减少页面首次加载http请求的次数)

- preload=auto 页面首次加载的时候就把音频资源进行加载
- preload=metadata 页面首次加载的时候只能音视资源的头部信息进行加载

<a name="59738ecf"></a>
### 4.2 尽量少用iframe
　　用iframe可以把一个HTML文档插入到父文档里，重要的是明白iframe是如何工作的并高效地使用它。<br />`<iframe>`的优点：

- 引入缓慢的第三方内容，比如标志和广告
- 安全沙箱
- 并行下载脚本

`<iframe>`的缺点：

- 代价高昂，即使是空白的iframe
- 阻塞页面加载
- 非语义

<a name="d501e480"></a>
### 4.3 杜绝404
　　HTTP请求代价高昂，完全没有必要用一个HTTP请求去获取一个无用的响应（比如404 Not Found），只会拖慢用户体验而没有任何好处。<br />　　有些站点用的是有帮助的404——“你的意思是xxx？”，这样做有利于用户体验，，但也浪费了服务器资源（比如数据库等等）。最糟糕的是链接到的外部JavaScript有错误而且结果是404。首先，这种下载将阻塞并行下载。其次，浏览器会试图解析404响应体，因为它是JavaScript代码，需要找出其中可用的部分。
