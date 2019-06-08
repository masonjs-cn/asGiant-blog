---
title: 1 css引入与规范
date: 2019-04-28 18:19:05
tags: css入门
desc: 
# keywords: 
categories:
  - css入门
# from: https://bitsofco.de/the-background-properties/
# demo: ../../../demos/201703/background.html
---

### 1.1 导入式
导入式会在整个网页装载完后再装载CSS文件，因此这就导致了一个问题，如果网页比较大则会儿出现先显示无样式的页面，闪烁一下之后，再出现网页的样式。这是导入式固有的一个缺陷。

```html
<style type="text/css" media="screen">   
	@import url("CSS文件");   
</style>
```
<br />
<a name="3e752127"></a>
### 1.2 外链式
引入一个外部的css样式表<br />语言:link标签 href="css样式路径名称" 可以放在head标签或者body标签里面

```javascript
<link rel="stylesheet" type="text/css" href="index.css">
```

<a name="ea268ffe"></a>
### 1.3 外链式和导入式的区别

- link和@import虽然都是引入外部的css文件，但是他们是有天差地别的区别的
- link是html标签，@import完全是css提供的方式，要写在css文件或者style标签中。
- 他们的加载顺序也是有区别的，当一个页面被加载的时间，link引用的css文件会被同时加载，而@import引入的css文件会等页面全部下载完后再加载。
- 当使用JavaScript控制DOM去改变css样式的时间，只能使用link标签，因为import是不能被DOM控制的

<a name="41d63a8b"></a>
### 1.4 行内式
> 通过style这个标签属性，将css键值对直接写入标签内


```html
<p style="width:100px;height:100px;background-color:red;"</p>
```

<a name="93b452a1"></a>
### 1.5 内嵌式
可以放在head或者body里 建议放在head标签里面title标签的下面<style><br />

```html
<style type="text/css">
  选择器{
  	声明;
    声明;
    ....
  }
</style>
```

<a name="bxENs"></a>
### 1.6 css的代码规范

- 必须使用英文开头，硬切开头字母一律小写
- 所有的命名最好都小写
- 尽量不要用缩写英文，除非可以一目了然的
- 如果遇到相差不大class或者id，主功能识别字母在钱，位置识别字母在后，位置识别字母第一个可大写（如：navTop，menuLeft）
- 遵循驼峰命名法:第一个单词的首字母小写，其余每一个有意义的单词的首字母大写(如:studentInfo、getElementById)

