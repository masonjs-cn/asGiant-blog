---
title: 10 全局api-nextTick
date: 2019-05-15 20:10:04
tags: Vue基础入门笔记
# desc: 作用域就是变量的作用范围。也就是你声明一个变量以后，这个变量可以在什么场合下使用。以前的JavaScript只有全局作用域，和函数作用域。
# keywords: 
categories:
  - Vue基础入门笔记
# from: https://bitsofco.de/the-background-properties/
# demo: ../../../demos/201703/background.html
---

## 官方说明
**参数**：

- `{Function} [callback]`
- `{Object} [context]`

**用法**：<br />
<br />在下次 DOM 更新循环结束之后执行延迟回调。在修改数据之后立即使用这个方法，获取更新后的 DOM。<br />

```javascript
// 修改数据
vm.msg = 'Hello'

// DOM 还没有更新
Vue.nextTick(function () {
  // DOM 更新了
})

// 作为一个 Promise 使用 (2.1.0 起新增，详见接下来的提示)
Vue.nextTick()
  .then(function () {
    // DOM 更新了
})
```

> 2.1.0 起新增：如果没有提供回调且在支持 Promise 的环境中，则返回一个 Promise。请注意 Vue 不自带 Promise 的 polyfill，所以如果你的目标浏览器不原生支持 Promise (IE：你们都看我干嘛)，你得自己提供 polyfill。


<a name="z6MNr"></a>
## 示例
先来一个示例了解下关于Vue中的DOM更新以及`nextTick`的作用。<br />**模板**
```javascript
<div class="app">
  <div ref="msgDiv">{{msg}}</div>
  <div v-if="msg1">Message got outside $nextTick: {{msg1}}</div>
  <div v-if="msg2">Message got inside $nextTick: {{msg2}}</div>
  <div v-if="msg3">Message got outside $nextTick: {{msg3}}</div>
  <button @click="changeMsg">
    Change the Message
  </button>
</div>
```

**Vue实例**<br />**
```javascript
new Vue({
  el: '.app',
  data: {
    msg: 'Hello Vue.',
    msg1: '',
    msg2: '',
    msg3: ''
  },
  methods: {
    changeMsg() {
      this.msg = "Hello world."
      this.msg1 = this.$refs.msgDiv.innerHTML
      this.$nextTick(() => {
        this.msg2 = this.$refs.msgDiv.innerHTML
      })
      this.msg3 = this.$refs.msgDiv.innerHTML
    }
  }
})
```

点击前

![image.png](https://cdn.nlark.com/yuque/0/2019/png/271124/1560262857808-3104fda4-8d22-400d-9ebf-ea86d582190d.png#align=left&display=inline&height=56&name=image.png&originHeight=112&originWidth=294&size=33721&status=done&width=147)

点击后

![image.png](https://cdn.nlark.com/yuque/0/2019/png/271124/1560262879570-c38932c1-2ea8-4772-af2a-0bd6efd55bf8.png#align=left&display=inline&height=116&name=image.png&originHeight=232&originWidth=688&size=206614&status=done&width=344)

> 从图中可以得知：msg1和msg3显示的内容还是变换之前的，而msg2显示的内容是变换之后的。其根本原因是因为Vue中DOM更新是异步的（详细解释在后面）。


<a name="QPiKI"></a>
## 应用场景

下面了解下`nextTick`的主要应用的场景及原因。

- 在Vue生命周期的`created()`钩子函数进行的DOM操作一定要放在`Vue.nextTick()`的回调函数中

在`created()`钩子函数执行的时候DOM 其实并未进行任何渲染，而此时进行DOM操作无异于徒劳，所以此处一定要将DOM操作的js代码放进`Vue.nextTick()`的回调函数中。与之对应的就是`mounted()`钩子函数，因为该钩子函数执行时所有的DOM挂载和渲染都已完成，此时在该钩子函数中进行任何DOM操作都不会有问题 。

- 在数据变化后要执行的某个操作，而这个操作需要使用随数据改变而改变的DOM结构的时候，这个操作都应该放进`Vue.nextTick()`的回调函数中。

具体原因在Vue的官方文档中详细解释:

> Vue 异步执行 DOM 更新。只要观察到数据变化，Vue 将开启一个队列，并缓冲在同一事件循环中发生的所有数据改变。如果同一个 watcher 被多次触发，只会被推入到队列中一次。这种在缓冲时去除重复数据对于避免不必要的计算和 DOM 操作上非常重要。然后，在下一个的事件循环“tick”中，Vue 刷新队列并执行实际 (已去重的) 工作。Vue 在内部尝试对异步队列使用原生的 `Promise.then` 和`MessageChannel`，如果执行环境不支持，会采用 `setTimeout(fn, 0)`代替。
> 例如，当你设置`vm.someData = 'new value'`，该组件不会立即重新渲染。当刷新队列时，组件会在事件循环队列清空时的下一个“tick”更新。多数情况我们不需要关心这个过程，但是如果你想在 DOM 状态更新后做点什么，这就可能会有些棘手。虽然 Vue.js 通常鼓励开发人员沿着“数据驱动”的方式思考，避免直接接触 DOM，但是有时我们确实要这么做。为了在数据变化之后等待 Vue 完成更新 DOM ，可以在数据变化之后立即使用`Vue.nextTick(callback)` 。这样回调函数在 DOM 更新完成后就会调用。

