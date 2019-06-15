---
title: 15 动态绑定样式-v-bind
date: 2019-05-16 12:10:04
tags: Vue基础入门笔记
# desc: 作用域就是变量的作用范围。也就是你声明一个变量以后，这个变量可以在什么场合下使用。以前的JavaScript只有全局作用域，和函数作用域。
# keywords: 
categories:
  - Vue基础入门笔记
# from: https://bitsofco.de/the-background-properties/
# demo: ../../../demos/201703/background.html
---

### 13.1 对象语法
> :class 绑定的样式和class绑定的不冲突


<a name="sjdDk"></a>
#### 13.1.1 直接绑定一个data
```html
<div v-bind:class="{ active: isActive }"></div>
```

> `active` 这个 class 存在与否将取决于数据属性 `isActive` 的 布尔值


```html
<div class="static" v-bind:class="{ active: isActive, 'text-danger': hasError }"></div>
```

<a name="gWlih"></a>
#### 13.1.2 data中使用一个对象绑定
```javascript
data: {
  classObject: {
    active: true,
    'text-danger': false
  }
}
```

<a name="I4eR3"></a>
#### 13.1.3 计算属性中绑定

```javascript
data: {
  isActive: true,
  error: null
},
computed: {
  classObject: function () {
    return {
      active: this.isActive && !this.error,
      'text-danger': this.error && this.error.type === 'fatal'
    }
  }
}
```

<a name="PROHG"></a>
### 13.2 数组语法

```html
<div v-bind:class="[activeClass, errorClass]"></div>
```

<a name="q3kqv"></a>
#### 13.2.1 直接动态绑定一个class

```javascript
data: {
  activeClass: 'active',
  errorClass: 'text-danger'
}
```

<a name="y375Y"></a>
#### 13.2.2 三元表达式

```html
<div v-bind:class="[isActive ? activeClass : '', errorClass]"></div>
```

不过，当有多个条件 class 时这样写有些繁琐。所以在数组语法中也可以使用对象语法：

```html
<div v-bind:class="[{ active: isActive }, errorClass]"></div>
```

