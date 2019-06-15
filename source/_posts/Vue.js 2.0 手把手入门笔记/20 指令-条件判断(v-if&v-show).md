---
title: 20 指令-条件判断(v-if&amp;v-show)
date: 2019-05-18 11:10:04
tags: Vue基础入门笔记
# desc: 作用域就是变量的作用范围。也就是你声明一个变量以后，这个变量可以在什么场合下使用。以前的JavaScript只有全局作用域，和函数作用域。
# keywords: 
categories:
  - Vue基础入门笔记
# from: https://bitsofco.de/the-background-properties/
# demo: ../../../demos/201703/background.html
---

## 1 v-if&v-show
- 条件渲染 (使用 `v-if`)
- 条件展示 (使用 `v-show`)
> if操作的是dom show 操作的样式
> 如果频繁切换dom使用v-show,当数据一开时就确定下来使用v-if更好一些,如果if通过内部指令不会执行了
> 只有dom从显示到隐藏 或者隐藏到显示 才能使用vue的动画


```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title>vue</title>
</head>
<body>
    <div id="app">
        <span v-if="flag">你看的见我</span>
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

<a name="TK71d"></a>
## 2 区别总结

- v-show:操作的是元素的display属性
- v-if:操作的是元素的创建和插入
- 相比较而言v-show的性能要高

