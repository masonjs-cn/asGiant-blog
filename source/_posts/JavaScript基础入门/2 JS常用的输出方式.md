---
title: 2.JS常用的输出方式
date: 2019-04-09 14:10:04
tags: JavaScript基础入门
desc: 
# keywords: 
categories:
  - JavaScript基础入门
# from: https://bitsofco.de/the-background-properties/
# demo: ../../../demos/201703/background.html
---

## 弹窗输出

### alert

- 在浏览器中弹出一个提示框(提供确定按钮，点击确定弹窗消失)
- 使用alert弹窗信息，提示的内容最后都会转换成字符串(调用了toSring这个方法)
```javascript
alert(1)
alert({name:'wjw'}) //=> '[object Object]'
alert([13,14]) //=> '12,13'
```

### confirm

- 在alert基础上增加了让用户选择的操作(提供两个按钮:确定和取消)
- 当用户点击确定按钮的时候，我们接收到的结果是true，点击是取消按钮我们接受到的结果是false，此后我们可以根据结果来处理即可 
```javascript
var wjw = confirm("are you sure");
alert(wjw);
```

### prompt

- - 在confirm 基础上增加让用户增加输入的效果
- - 用户点击取消按钮，我们获取到的结果是null,如果用户点击是确定按钮，我们将获取用户输入的信息
- - 在真实的项目中，一般性会使用二次封装的弹窗，不会使用这种弹窗

```javascript
var flag = prompt("are you sure");

alert(flag)
```

## 控制台输出
> 控制台输出，方便开发调试

### console

- 在控制台输出，优势不会转换数据类型，输出什么格式的数据都可以

```javascript
console.log({name:'wjw'});

console.dir() //比log输出更加详细一些
console.table //把json数据展示成一个表格
```


