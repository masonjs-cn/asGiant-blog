---
title: 14 插槽-slot
date: 2019-05-16 11:10:04
tags: Vue基础入门笔记
# desc: 作用域就是变量的作用范围。也就是你声明一个变量以后，这个变量可以在什么场合下使用。以前的JavaScript只有全局作用域，和函数作用域。
# keywords: 
categories:
  - Vue基础入门笔记
# from: https://bitsofco.de/the-background-properties/
# demo: ../../../demos/201703/background.html
---

### 老版本vue
> 模板中只能有一个根元素

    
> HTML内容模板（<template>）元素是一种用于保存客户端内容机制，该内容在加载页面时不会呈现，但随后可以在运行时使用JavaScript实例化。

    
```html
<div id="app">
   <modal></modal> 
</div>

<template id="modal">
   <div>
     <h1>是否删除</h1>
  </div>
</template>
```

```javascript
let modal = {
 template:"#modal"
}

const app = new Vue({
 el:'#app',
 components:{
   modal
 },
 data:{
 }
})
```

> 我们通常是想把h1的值动态放入，所以就要用到插槽


<a name="4wvW6"></a>
#### 单个插槽 | 默认插槽 | 匿名插槽
> 首先是单个插槽，**单个插槽**是vue的官方叫法，但是其实也可以叫它默认插槽，或者与具名插槽相对，我们可以叫它匿名插槽。因为它不用设置name属性。
> 单个插槽可以放置在组件的任意位置，但是就像它的名字一样，一个组件中只能有一个该类插槽。相对应的，具名插槽就可以有很多个，只要名字（name属性）不同就可以了。


```html
<div id="app">
  <modal>
    <h1>插入成功</h1>
  </modal>
</div>

<template id="modal">
  <div>
    <slot></slot>
  </div>
</template>
```


![image.png](https://cdn.nlark.com/yuque/0/2019/png/271124/1560398287016-d8f986a7-505e-44ce-ba6a-5b266d838876.png#align=left&display=inline&height=57&name=image.png&originHeight=114&originWidth=286&size=3695&status=done&width=143)

> 当我们看到插入成功的时候，匿名插入就实现了


<a name="W4O9O"></a>
#### 具名插槽
> 匿名插槽没有name属性，所以是匿名插槽，那么，插槽加了name属性，就变成了具名插槽。具名插槽可以在一个组件中出现N次，出现在不同的位置。下面的例子，就是一个有两个**具名插槽**和**单个插槽**的组件，这三个插槽被父组件用同一套css样式显示了出来，不同的是内容上略有区别。


> 简单的来说，就是，我们可能遇到一个问题
> 我们想插入不同的插槽内的内容不一样


> 在 2.6.0+ 中已弃用


```html
<div id="app">
    <modal>
        <h1>插入成功</h1>
        <h2 slot="title">标题</h2>
        <h2 slot="content">内容</h2>
    </modal>
</div>

<template id="modal">
  <div>
    <slot name="default"></slot>
    <slot name="title"></slot>
    <slot name="content"></slot>
  </div>
</template>
```

> 我们可以发现没有name的情况下，默认就是default


<a name="j4pc4"></a>
#### 作用域插槽 | 带数据的插槽
> 最后，就是我们的作用域插槽。这个稍微难理解一点。官方叫它作用域插槽，实际上，对比前面两种插槽，我们可以叫它带数据的插槽。什么意思呢，就是前面两种，都是在组件的template里面写


> 在 2.6.0+ 中已弃用

<br />
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>Vue作用域插槽</title>
    <script src="https://cdn.bootcss.com/vue/2.3.4/vue.js"></script>
</head>

<body>
    <div id="app2">
        <!-- 组件使用者只需传递users数据即可 -->
        <my-stripe-list :items="users" odd-bgcolor="#D3DCE6" even-bgcolor="#E5E9F2">
            <!-- props对象接收来自子组件slot的$index参数 -->
            <template slot="cont" scope="props">
                <span>{{users[props.$index].id}}</span>
                <span>{{users[props.$index].name}}</span>
                <span>{{users[props.$index].age}}</span>
                <!-- 这里可以自定[编辑][删除]按钮的链接和样式 -->
                <a :href="'#edit/id/'+users[props.$index].id">编辑</a>
                <a :href="'#del/id/'+users[props.$index].id">删除</a>
            </template>
        </my-stripe-list>
    </div>
    <script>
        Vue.component('my-stripe-list', {
            /*slot的$index可以传递到父组件中*/
            template: `
                    <div>
                        <div v-for="(item, index) in items" style="line-height:2.2;" :style="index % 2 === 0 ? 'background:'+oddBgcolor : 'background:'+evenBgcolor">
                            <slot name="cont" :$index="index"></slot>
                        </div>
                    </div>
                `,
            props: {
                items: Array,
                oddBgcolor: String,
                evenBgcolor: String
            }
        });
        new Vue({
            el: '#app2',
            data: {
                users: [{
                        id: 1,
                        name: '张三',
                        age: 20
                    },
                    {
                        id: 2,
                        name: '李四',
                        age: 22
                    },
                    {
                        id: 3,
                        name: '王五',
                        age: 27
                    },
                    {
                        id: 4,
                        name: '张龙',
                        age: 27
                    },
                    {
                        id: 5,
                        name: '赵虎',
                        age: 27
                    }
                ]
            }
        });
    </script>
</body>

</html>
```

> 这种写法，习惯了element-ui的朋友一定就很熟悉了。


总结： <br />1 . 使用slot可以在自定义组件内插入原生HTML元素，需要搭配使用name和slot属性，否则多个slot可能会返回重复的HTML元素。<br />2 . 使用slot-scope可以将slot内部的作用域指向该子组件，否则默认作用域指向调用slot的父组件。

<a name="7jdib"></a>
### 新版本的 v-slot
> 从 [vue@2.6.x](https://link.juejin.im?target=https%3A%2F%2Fgithub.com%2Fvuejs%2Fvue%2Freleases%2Ftag%2Fv2.6.0) 开始，Vue 为具名和范围插槽引入了一个全新的语法，即我们今天要讲的主角：`v-slot` 指令。目的就是想统一 `slot` 和 `scope-slot` 语法，使代码更加规范和清晰。既然有新的语法上位，很明显，`slot` 和 `scope-slot` 也将会在 `vue@3.0.x` 中彻底的跟我们说拜拜了。而从 `vue@2.6.0` 开始，官方推荐我们使用 `v-slot` 来替代后两者。

<br />
<a name="1YDts"></a>
#### 具名插槽
> 实例化一个vue


```javascript
// 组件
Vue.component('lv-hello', {
  template: `
    <div>
      <slot name="header"></slot>
      <h1>我的天呀</h1>
    </div>`
})

new Vue({
  el: '#app1',
  data: {

  }
});
```

> 老版本


```html
<div id="app1">
  <!-- 老版本使用具名插槽 -->
  <lv-hello>
    <p slot="header">我是头部</p>
  </lv-hello>
</div>
```

> 新版本的变化


```html
  <!-- 新版本使用具名插槽 -->
  <lv-hello>
    <!-- 注意：这块的 v-slot 指令只能写在 template 标签上面，而不能放置到 p 标签上 -->
    <template v-slot:header>
      <p>我是头部</p>
    </template>
  </lv-hello>
</div>
```

<a name="COUF6"></a>
#### 具名插槽的缩写

> 将 `v-slot:` 替换成 `#` 号


```html
<div id="app">
  <lv-hello>
    <template #header>
      <p>我是头部</p>
    </template>
    <!-- 注意: #号后面必须有参数，否则会报错。即便是默认插槽，也需要写成 #default -->
    <template #default>
      <p>我是默认插槽</p>
    </template>
  </lv-hello>
</div>
```

<a name="TLyxU"></a>
#### 作用域插槽
> 所谓作用域插槽，就是让插槽的内容能够访问子组件中才有的数据。


```javascript
Vue.component('lv-hello', {
  data: function () {
    return {
      firstName: '张',
      lastName: '三'
    }
  },

  template: `
    <div>
      <slot name="header" :firstName="firstName" :lastName="lastName"></slot>
      <h1>我的天呀</h1>
    </div>
  `
})
```

```html
<div id="app">
  <!-- 老版本使用具名插槽 -->
  <lv-hello>
  	<p slot="header" slot-scope="hh">我是头部 {{ hh.firstName }} {{ hh.lastName }}</p>
	</lv-hello>
<!-- 新版本使用具名插槽 -->
    <lv-hello>
      <!-- 注意：这块的 v-slot 指令只能写在 template 标签上面，而不能放置到 p 标签上 -->
      <template v-slot:header="hh">
         <p>我是头部 {{ hh.firstName }} {{ hh.lastName }}</p>
      </template>
  	</lv-hello>
</div>
```

