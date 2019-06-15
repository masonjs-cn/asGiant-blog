---
title: 23 实例属性-$ref
date: 2019-05-18 15:10:04
tags: Vue基础入门笔记
# desc: 作用域就是变量的作用范围。也就是你声明一个变量以后，这个变量可以在什么场合下使用。以前的JavaScript只有全局作用域，和函数作用域。
# keywords: 
categories:
  - Vue基础入门笔记
# from: https://bitsofco.de/the-background-properties/
# demo: ../../../demos/201703/background.html
---

## 官网针对-ref的解释
- **预期**：`string`<br />`ref` 被用来给元素或子组件注册引用信息。引用信息将会注册在父组件的 `$refs` 对象上。如果在普通的 DOM 元素上使用，引用指向的就是 DOM 元素；如果用在子组件上，引用就指向组件实例：
```
<!-- `vm.$refs.p` will be the DOM node -->
<p ref="p">hello</p>
<!-- `vm.$refs.child` will be the child component instance -->
<child-component ref="child"></child-component>
```

- 当 `v-for` 用于元素或组件的时候，引用信息将是包含 DOM 节点或组件实例的数组。<br />关于 ref 注册时间的重要说明：因为 ref 本身是作为渲染结果被创建的，在初始渲染的时候你不能访问它们 - 它们还不存在！`$refs` 也不是响应式的，因此你不应该试图用它在模板中做数据绑定。

<a name="P2AYt"></a>
## 操作dom
> 如果我们用jQuery的话,一般性都可以操作dom


```javascript
$("#id").text('xxx')   // 使用Jquery
document.getElementById("id")  // 使用原生Dom
```

现在我们牛逼了，我们用vue。那vue中，如果我要获取Dom，该怎么做？<br />这就进入本文的主题ref, $refs，官网解释：

```html
<div id="app">
   <div>{{msg}}</div>
</div>
```

> 在JavaScript中我们习惯了使用document.getElementsByTagName

<br />
```javascript
var vm = new Vue({
  el: '#app',
  data:{
    msg:'hello'
  },
  mounted() {
    console.log(document.getElementsByTagName("div")[0].innerHTML);
  }
})
```

<a name="noZkB"></a>
## vue操作dom
> 那么我们在vue中呢


```html
<div id="app">
   <div ref="msg">{{msg}}</div>
</div>
```

```javascript

    var vm = new Vue({
      el: '#app',
      data:{
        msg:'hello'
      },
      mounted() {
        // console.log(document.getElementsByTagName("div")[0].innerHTML);
        console.log('====================================');
        console.log(this.$refs.msg);
        console.log('====================================');
      }
    })
```


