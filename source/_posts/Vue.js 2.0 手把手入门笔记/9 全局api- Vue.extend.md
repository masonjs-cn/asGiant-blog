---
title: 9 全局api- Vue.extend
date: 2019-05-15 19:10:04
tags: Vue基础入门笔记
# desc: 作用域就是变量的作用范围。也就是你声明一个变量以后，这个变量可以在什么场合下使用。以前的JavaScript只有全局作用域，和函数作用域。
# keywords: 
categories:
  - Vue基础入门笔记
# from: https://bitsofco.de/the-background-properties/
# demo: ../../../demos/201703/background.html
---

> 使用基础 Vue 构造器，创建一个“子类”。参数是一个包含组件选项的对象。


`data` 选项是特例，需要注意 - 在 `Vue.extend()` 中它必须是函数

```javascript
<div id="mount-point"></div>
```

```javascript
// 创建构造器
var demo = Vue.extend({
  template: '<p>{{firstName}} {{lastName}} aka {{alias}}</p>',
  data: function () {
    return {
      firstName: 'Walter',
      lastName: 'White',
      alias: 'Heisenberg'
    }
  }
})

// 创建 Profile 实例，并挂载到一个元素上。
new demo().$mount('#mount-point')
```


