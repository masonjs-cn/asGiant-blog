---
title: 3.JS定义值
date: 2019-04-09 15:10:04
tags: JavaScript基础入门
desc: 
# keywords: 
categories:
  - JavaScript基础入门
# from: https://bitsofco.de/the-background-properties/
# demo: ../../../demos/201703/background.html
---

语法
ECMAScript 的语法大量借鉴了 C 及其他类 C 语言（如 Perl 和 Java）的语法。
区分大小写

## 注释

```javascript
// 单行注释

/*
*	 这是一个多行
*	（块级）注释
*/
```

## 严格模式
严格模式
ES5 引入了严格模式的概念，在严格模式下，ES3 中的一些不确定行为将得到处理，而且队某些不安全的操作也会抛出错误。要在整个脚本中启用严格模式，可以在顶部添加如下代码：<br />这行代码看起来像是字符串，而且也没有赋值给任何变量，但其实它是一个编译指
示（pragma），用于告诉支持的JavaScript引擎切换到严格模式。在函数内部的上方包含这条编译指示，也可以指定函数在严格模式下执行:

```javascript
function doSomething(){
 	"use strict";  //函数体
}
```

## 变量、常量
> 变量是可以变得
> 常量是不可变的


### 变量

- 变量其实只是一个无意义的名字，它所代表的意义都是其存储的那个值
- 让原有的num变量存储的值修改为13（变量只能代表一值）

js定义变量的方法

```javascript
// var 变量名 = 值;

var num = 12;
var name = 'wjw'
```

### 常量

- 任何一个具体的数据都是常量，例如12是个常量
- 和变量累死，我们设置一个常量（也就是一个名字），给其存储一个值，但是这个存储的值不能修改

```javascript
const num = 12;
```

## JS中命名规范

- JS中严格区分大小写

```javascript
var test = 'wjw';
var Test = 'wjh';
console.log(test);
// 输出test
```

- 遵循国际命名规则"驼峰命名法"
> 第一个单词首字母小写，其余每一个有意义单词首字母大写


```javascript
var studentInfo; // 学生信息
// 所见即所得
// 例子:

/*
*	 info : information 信息
*	 init : initlization 初始化
*  add/insert/create 增加插入创建
*  remove/rm/clear/del/delete 删除
*  update 修改
*  get/query/select : 查询获取
*/
```

- 命名的时候可以使用$、_、数字、字母，但是数字不能作为名字的第一位

```javascript
var student_info;
var $xxx; //=> 一般都是应用jq获得到的值
var _xxx; //=> 一般这样的情况代表变量是一个局或者公共的变量
```

- JS中很多字都是有特殊含义的，我们这些词，叫做关键词；现在没有特殊含义，以后可能会作为关键的，我们叫做保留字；二关键词和保留字不可以随便用来命名；

![image.png](https://cdn.nlark.com/yuque/0/2019/png/271124/1552036896263-fd04e4f8-345d-4ff6-9587-45c3a1a67877.png#align=left&display=inline&height=277&name=image.png&originHeight=554&originWidth=1336&size=284246&status=done&width=668)<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/271124/1552036875298-debe0648-b2cf-484c-8069-43111c9cf872.png#align=left&display=inline&height=610&name=image.png&originHeight=1220&originWidth=1660&size=696625&status=done&width=830)<br />
