---
title: 2 vue基础指令
date: 2019-05-15 12:10:04
tags: Vue基础入门笔记
# desc: 作用域就是变量的作用范围。也就是你声明一个变量以后，这个变量可以在什么场合下使用。以前的JavaScript只有全局作用域，和函数作用域。
# keywords: 
categories:
  - Vue基础入门笔记
# from: https://bitsofco.de/the-background-properties/
# demo: ../../../demos/201703/background.html
---

## 2.1 安装vue
- cnd方式
> <script src="https://cdn.jsdelivr.net/npm/vue"></script>

- npm 方式

## 2.2 简单的尝试
> 这里使用cnd方便测试

```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8" />
    <title>vue</title>
</head>

<body>
    <div id="content">
        <!-- moustache 小胡子语法 表达式 可以放赋值 取值 三元-->
        {{ msg }}
    </div>
</body>
<script src="https://cdn.jsdelivr.net/npm/vue"></script> 
<!-- 使用官网的vue地址 -->
<script>
    // 引用vue后会给一个vue构造函数
    var vm = new Vue({ // vm === viewModel
        el: '#content', // 告诉vue管理哪一部分,querySelector "document.querySelector("#content")"
        data: { // data中的数据会被vm所代理
            msg: 'Hello Vue!' // 可以通过vm.msg获取对应的呢日用
        }
    })// Object.defineProperty
    vm.msg = "wjw" // 修改视图
</script>
</html>
```

![image.png](https://cdn.nlark.com/yuque/0/2019/png/271124/1557821762435-5cc94d74-2309-4460-a66c-b42718784e2f.png#align=left&display=inline&height=396&name=image.png&originHeight=244&originWidth=460&size=38937&status=done&width=746)
<a name="EPbHR"></a>
## 2.3 模板语法
> 综上所属得出了一套模板语法

<a name="FLYvx"></a>
### 2.3.1 文本
```html
<span>Message:{{msg}}</span>
```

<a name="xw5it"></a>
### 2.3.2 表达式
```
{{number + 1}}
{{ok?'YES':'NO'}}
{{message.split('').reverse().join('')}}
```

> 但是vue的表单元素 input checkbox textarea radio select 非文本处理
> 
> vue的指令 directive 只是dom上的行间属性，vue给这类属性赋予了一些意义，来实现特殊功能所有指令都以v-开头value属性默认情况下回vue忽略掉 selected checked 都没有意义

<a name="wv9nE"></a>
### 
<a name="mEXpo"></a>
### 2.3.3表单输入
> v-model 会将msg赋予输入框，输入框的值改变会影响数据

```html
<input v-model="msg">
<input type="checkbox" v-model="msg1" value="爬山">
```

<a name="74eXy"></a>
### 2.3.4 原始HTML

```html
<p>Using mustache:<span v-html='rawHtml'></spn></p>
```

<a name="dLDmQ"></a>
### 2.3.5 指令

```html
<p v-if='seen'>现在看到我了</p>
```

<a name="9mAHb"></a>
### 2.3.6 特性
```html
<div v-bind:id='dynamicld'></div>
```

<a name="6ujo3"></a>
## 2.4 Object.defineProperty原理

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title>vue</title>
</head>
<body>
    <div id="content"></div>
    <input type="text" id="input">
</body>
  
<script>
    let obj = {}
    let temp = {};
    document.getElementById("content").innerHTML = obj.name
    // 'name' 代表属性
    Object.defineProperty(obj,'name',{
        configurable:false, //是否可删除
        // writable:true,// 是否可赋值(如果使用set方法,则不能使用)
        enumerable:true, // 是否可枚举,也是就for..in..
        // value:1,// 值(如果使用get方法,则不能使用)
        get(){ // 取obj的name会触发get方法
            return temp['name']
        },
        set(val){// 给obj赋值会触发get方法
            // console.log(val);
            temp['name'] = val // 改变temp的结果
            input.value = val // 将值赋值给输入框
        }
    });
    input.value = obj.name // 页面一加载，会将调用get方法
    input.addEventListener('input',function(){ // 等待输入框的变化
        obj.name = this.value // 当值变化时会调用set方法
        document.getElementById("content").innerHTML = obj.name
    })
</script>

</html>
```

![image.png](https://cdn.nlark.com/yuque/0/2019/png/271124/1557825100635-9c7ad9d3-7424-4a48-be61-a27143c1c421.png#align=left&display=inline&height=53&name=image.png&originHeight=106&originWidth=334&size=4802&status=done&width=167)

最后可以实现双向绑定的雏形


