---
title: 21 内置组件-动画(transition)
date: 2019-05-18 13:10:04
tags: Vue基础入门笔记
# desc: 作用域就是变量的作用范围。也就是你声明一个变量以后，这个变量可以在什么场合下使用。以前的JavaScript只有全局作用域，和函数作用域。
# keywords: 
categories:
  - Vue基础入门笔记
# from: https://bitsofco.de/the-background-properties/
# demo: ../../../demos/201703/background.html
---

### 1 组件的过渡
Vue 提供了 `transition` 的封装组件，在下列情形中，可以给任何元素和组件添加进入/离开过渡

![image.png](https://cdn.nlark.com/yuque/0/2019/png/271124/1557903741434-1d5cce33-0862-4832-b272-67d9825bfe7e.png#align=left&display=inline&height=249&name=image.png&originHeight=498&originWidth=1162&size=45263&status=done&width=581)

在进入/离开的过渡中，会有 6 个 class 切换。

1. `v-enter`：定义进入过渡的开始状态。在元素被插入之前生效，在元素被插入之后的下一帧移除。<br />
1. `v-enter-active`：定义进入过渡生效时的状态。在整个进入过渡的阶段中应用，在元素被插入之前生效，在过渡/动画完成之后移除。这个类可以被用来定义进入过渡的过程时间，延迟和曲线函数。<br />
1. `v-enter-to`: **2.1.8版及以上** 定义进入过渡的结束状态。在元素被插入之后下一帧生效 (与此同时 `v-enter` 被移除)，在过渡/动画完成之后移除。<br />
1. `v-leave`: 定义离开过渡的开始状态。在离开过渡被触发时立刻生效，下一帧被移除。<br />
1. `v-leave-active`：定义离开过渡生效时的状态。在整个离开过渡的阶段中应用，在离开过渡被触发时立刻生效，在过渡/动画完成之后移除。这个类可以被用来定义离开过渡的过程时间，延迟和曲线函数。<br />
1. `v-leave-to`: **2.1.8版及以上** 定义离开过渡的结束状态。在离开过渡被触发之后下一帧生效 (与此同时 `v-leave` 被删除)，在过渡/动画完成之后移除。<br />
<a name="QYFv7"></a>
#### 1.1 初步代码实现
```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title>vue</title>
</head>
<style>
    div>div{
        width:100px;height: 100px;background: red;
    }
    .v-enter{
        opacity: 1;
    }
    /* 激活的时候 */
    .v-enter-avtive{
        opacity: 0;
        transition: 1s linear;
    }
    /* 离开 */
    .v-leave-active{
        opacity: 0;
        background: black;
        transition: 1s linear;
    }
</style>
<body>
    <div id="app">
        <button @click="flag=!flag">切换</button>
        <!-- vue自定义的组件 -->
        <transition>
            <div v-show="flag"></div>
        </transition>
    </div>
</body>
<script src="https://cdn.jsdelivr.net/npm/vue"></script> 
<script>
    var vm = new Vue({
        el:'#app',
        data:{
            flag:true
        }
    })
</script>
</html>
```

<a name="OEs6Z"></a>
#### 1.2 多个transition
> 遇上了多个transition的时候，同一个class肯定是会冲突的，那么如何处理呢


```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title>vue</title>
</head>
<style>
    div>div{
        width:100px;height: 100px;background: red;
    }
    .jw-enter-active {
        transition: all .3s ease;
    }
    .jw-leave-active {
        transition: all .8s cubic-bezier(1.0, 0.5, 0.8, 1.0);
    }
    .jw-enter, .jw-leave-to
    {
        transform: translateX(10px);
        opacity: 0;
    }
</style>
<body>
    <div id="app">
        <button @click="flag=!flag">切换</button>

        <!-- vue自定义的组件 -->
        <transition name="jw">
            <div v-show="flag"></div>
        </transition>
    </div>
</body>
<script src="https://cdn.jsdelivr.net/npm/vue"></script> 
<script>
    var vm = new Vue({
        el:'#app',
        data:{
            flag:true
        }
    })
</script>
</html>
```

简单的理解就是就 transition有一个name属性<br />在css中name-状态即可调用
