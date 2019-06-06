---
title: 1.导入JS
date: 2019-04-09 13:10:04
tags: JavaScript基础入门
desc: 作用域就是变量的作用范围。也就是你声明一个变量以后，这个变量可以在什么场合下使用。以前的JavaScript只有全局作用域，和函数作用域。
# keywords: 
categories:
  - JavaScript基础入门
# from: https://bitsofco.de/the-background-properties/
# demo: ../../../demos/201703/background.html
---

## 三种常见导入

### 行内导入JS(慎重：不安全)

```html
<div onclick="alert('hello world')"></div>
```

### 内嵌式

```html
<script>
	alert('hello world')
</script>
```

### 外链式

```html
// 新建一个js文件
<script src="./js/demo.js"></script>

// or

<script src="./js/demo.js" type="text/javascript"></script>
```

## 内嵌与外链不能同时操作
> 内嵌导入和外链导入不能合并在一起，如果当前是外链导入的，那么在script脚本块找那个编写的所有代码都不会被执行。


```javascript
<script src="./js/demo.js">
  alert('hello world')
</script>
```

## 位置编写位置
> 我们一般性会把css放在body的上面，把js放在body末尾(约定速成的规范)


    但是如果放在了标签前面那么将如何处理?
> 页面加载完所有资源之后执行操作


 在js中

```javascript
window.onload=function(){

}

```

在jq中

```javascript
$(document).ready(function(){

})

window.addEventListener('load',function(){},false);

// ie8以下

window.attachEvent('onreadystatechange',function(){
})
```

