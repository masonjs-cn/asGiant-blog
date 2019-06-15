---
title: 13 全局api-fifer过滤器
date: 2019-05-15 23:10:04
tags: Vue基础入门笔记
# desc: 作用域就是变量的作用范围。也就是你声明一个变量以后，这个变量可以在什么场合下使用。以前的JavaScript只有全局作用域，和函数作用域。
# keywords: 
categories:
  - Vue基础入门笔记
# from: https://bitsofco.de/the-background-properties/
# demo: ../../../demos/201703/background.html
---

### 8.1 介绍
允许你自定义过滤器，可被用于一些常见的文本格式化。过滤器可以用在两个地方：**双花括号插值和 `v-bind` 表达式** (后者从 2.1.0+ 开始支持)。过滤器应该被添加在 JavaScript 表达式的尾部，由“管道”符号指示

<a name="68P6e"></a>
### 8.2 优势
1、在Vue中使用过滤器（Filters）来渲染数据是一种很有趣的方式。<br />2、首先我们要知道，Vue中的过滤器不能替代Vue中的`methods`、`computed`或者`watch`，<br />3、过滤器不改变真正的`data`，而只是改变渲染的结果，并返回过滤后的版本。<br />4、在很多不同的情况下，过滤器都是有用的，比如尽可能保持API响应的干净，并在前端处理数据的格式。<br />5、在你希望避免重复和连接的情况下，它们也可以有效地封装成可重用代码块背后的所有逻辑。

<a name="laCN4"></a>
### 8.3 过滤器例子

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title>vue</title>
</head>
<body>
    <div id="app">
        <div>{{ message | capitalize }}</div>
    </div>
</body>
<script src="https://cdn.jsdelivr.net/npm/vue"></script> 
<script>
    var vm= new Vue({
      el: '#app',
      data: {
        message: 'world'
      },
      filters: { // 可以有好多的自定义过滤器
        capitalize(value) { // 这里的this指向的window
            if (!value) return ''
            value = value.toString()
            return value.charAt(0).toUpperCase() + value.slice(1)
        }
      }
    });
  </script>
</html>
```

<a name="OLJ0w"></a>
### 8.4 过滤器串连

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title>vue</title>
</head>
<body>
    <div id="app">
        {{ message | filterA | filterB }}
    </div>
</body>
<script src="https://cdn.jsdelivr.net/npm/vue"></script> 
<script>
    var vm= new Vue({
      el: '#app',
      data: {
        message: 'world'
      },
      filters: { // 可以有好多的自定义过滤器
        filterA(value){
            return value.split('').reverse().join('');
        },
        filterB(value){
            return value.charAt(0).toUpperCase() + value.slice(1)
        }
      }
    });
  </script>
</html>
```

<a name="0PiA1"></a>
### 8.5 过滤器传参

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title>vue</title>
</head>
<body>
    <div id="app">
        {{ message | filterA('hello',hi) }}
    </div>
</body>
<script src="https://cdn.jsdelivr.net/npm/vue"></script> 
<script>
    var vm= new Vue({
      el: '#app',
      data: {
        hi:'!',
        message: 'world'
      },
      filters: { // 可以有好多的自定义过滤器
        filterA(value1,value2,value3){
            return `${value2} ${value1} ${value3}`;
        }
      }
    });
  </script>
</html>
```

这里，filterA 被定义为接收三个参数的过滤器函数。其中 message 的值作为第一个参数，普通字符串 'hello' 作为第二个参数，表达式 hi 的值作为第三个参数。
