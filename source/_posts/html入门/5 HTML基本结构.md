---
title: 5 HTML基本结构
date: 2019-03-06 19:50:18
tags: html入门
desc: 
# keywords: 
categories:
  - html入门
# from: https://bitsofco.de/the-background-properties/
# demo: ../../../demos/201703/background.html
---

<a name="188dab1b"></a>
### 5.1 html基本结构
- HTML文档标记：<html>
- 头标签：<head>
- 标题标签：<title>
- 页面元信息：<meta>,一般设置为utf-8
- 主题标记：<body>

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Document</title>
</head>
<body>
</body>
</html>
```

<a name="cc34e3eb"></a>
### 5.2 HTML文档的后缀名
> .html与.htm均是静态网页后缀名，网页文件没有区别与区分，html与htm后缀网页后缀可以互换，对网页完全没有影响同时也没有区别。可以认为html与htm没有本质区别，唯一区别即多与少一个“L”。


<a name="ce6865bd"></a>
### 5.3 元素语法

- HTML 元素以开始标签起始
- HTML 元素以结束标签终止
- 元素的内容是开始标签与结束标签之间的内容
- 某些 HTML 元素具有空内容（empty content）
- 空元素在开始标签中进行关闭（以开始标签的结束而结束）
- 大多数 HTML 元素可拥有属性

<a name="d80f3319"></a>
### 5.4 嵌套的 HTML 元素
> HTML 文档由嵌套的 HTML 元素构成。大多数 HTML 元素可以嵌套（可以包含其他 HTML 元素）。


<a name="f6a33d1c"></a>
### 5.5 空元素

- 没有内容的 HTML 元素被称为空元素。空元素是在开始标签中关闭的。
- <br> 就是没有关闭标签的空元素（<br> 标签定义换行）。
- 在 XHTML、XML 以及未来版本的 HTML 中，所有元素都必须被关闭。
- 在开始标签中添加斜杠，比如 <br />，是关闭空元素的正确方法，HTML、XHTML 和 XML 都接受这种方式。
- 即使 <br> 在所有浏览器中都是有效的，但使用 <br/> 其实是更长远的保障。

<a name="04a1ebc2"></a>
### 5.6 HTML 标签大小写

- HTML 标签对大小写不敏感：<P> 等同于 <p>。许多网站都使用大写的 HTML 标签。
- PHP中文网使用的是小写标签，因为万维网联盟（W3C）在 HTML 4 中推荐使用小写，而在未来 (X)HTML 版本中强制使用小写。

<a name="464c20d4"></a>
### 5.7 HTML属性
虽然世界上存在一个万能标签div，但是还是需要一些特别的标签去完成一些特别的事情,例如 a标签中href属性 img标签中的src属性。
