---
title: 22 自定义指令-directives
date: 2019-05-18 14:10:04
tags: Vue基础入门笔记
# desc: 作用域就是变量的作用范围。也就是你声明一个变量以后，这个变量可以在什么场合下使用。以前的JavaScript只有全局作用域，和函数作用域。
# keywords: 
categories:
  - Vue基础入门笔记
# from: https://bitsofco.de/the-background-properties/
# demo: ../../../demos/201703/background.html
---

<a name="VpxwT"></a>
## 15.1 介绍
Vue 也允许注册自定义指令。注意，在 Vue2.0 中，代码复用和抽象的主要形式是组件。然而，有的情况下，你仍然需要对普通 DOM 元素进行底层操作，这时候就会用到自定义指令。<br />
<br />举一个栗子:
```javascript
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title>vue</title>
</head>
<body>
    <div id="app">
       <div v-color='flag'>123</div>
    </div>
</body>
<script src="https://cdn.jsdelivr.net/npm/vue"></script> 
<script>
    var vm = new Vue({
        directives:{
            color(el,bindings){ //el值指代的是button按钮
                console.log(arguments);
                el.style.background = bindings.value;
            }
        },
        el: '#app',
        data: {
            flag: 'red'
        },
        methods:{
            getSomething(){
                return "hello"
            }
        }
    })
</script>
</html>
```

出现如图情况

![image.png](https://cdn.nlark.com/yuque/0/2019/png/271124/1557979872661-82fbbe5f-21d7-4d27-b776-8e6da08f262e.png#align=left&display=inline&height=68&name=image.png&originHeight=136&originWidth=576&size=3491&status=done&width=288)

![image.png](https://cdn.nlark.com/yuque/0/2019/png/271124/1557981369618-255dc6df-0173-436d-8d90-4e3a08c08685.png#align=left&display=inline&height=164&name=image.png&originHeight=328&originWidth=1558&size=102694&status=done&width=779)

> 再来个栗子


```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title>vue</title>
</head>
<style>
    .a{
        position: absolute;width: 100px;height: 100px;background: red;
    }
</style>
<body>
    <div id="app">
       <div class="a" v-drag></div>
    </div>
</body>
<script src="https://cdn.jsdelivr.net/npm/vue"></script> 
<script>
    var vm = new Vue({
        directives:{
            drag(el){
                el.onmousedown = function (e) {
                    var disx = e.pageX - el.offsetLeft;
                    var disy = e.pageY - el.offsetTop;
                    document.onmousemove = function (e) {
                        el.style.left = e.pageX - disx +'px';
                        el.style.top = e.pageX - disy + 'px';
                    }

                    document.onmouseup = function (e) {
                        document.onmousemove = document.onmousemove = null;
                    }

                    e.preventDefault();
                }
            }
        },
        el: '#app',
        data: {
            flag: 'red'
        },
        methods:{
            getSomething(){
                return "hello"
            }
        }
    })
</script>
</html>
```

![image.png](https://cdn.nlark.com/yuque/0/2019/png/271124/1557981323722-a124890f-84be-46cd-841c-59bdaeecadf8.png#align=left&display=inline&height=251&name=image.png&originHeight=502&originWidth=1720&size=17097&status=done&width=860)

可以拖动

<a name="2MYal"></a>
## 15.2 钩子函数
一个指令定义对象可以提供如下几个钩子函数 (均为可选)：<br />`bind`：只调用一次，指令第一次绑定到元素时调用。在这里可以进行一次性的初始化设置。

`inserted`：被绑定元素插入父节点时调用 (仅保证父节点存在，但不一定已被插入文档中)。

`update`：所在组件的 VNode 更新时调用，但是可能发生在其子 VNode 更新之前。指令的值可能发生了改变，也可能没有。但是你可以通过比较更新前后的值来忽略不必要的模板更新 (详细的钩子函数参数见下)。

<a name="Zd937"></a>
## 15.3 钩子函数参数

- `el`：指令所绑定的元素，可以用来直接操作 DOM 。
- `binding`：一个对象，包含以下属性：
  - `name`：指令名，不包括 `v-` 前缀。
  - `value`：指令的绑定值，例如：`v-my-directive="1 + 1"` 中，绑定值为 `2`。
  - `oldValue`：指令绑定的前一个值，仅在 `update` 和 `componentUpdated` 钩子中可用。无论值是否改变都可用。
  - `expression`：字符串形式的指令表达式。例如 `v-my-directive="1 + 1"`中，表达式为 `"1 + 1"`。
  - `arg`：传给指令的参数，可选。例如 `v-my-directive:foo` 中，参数为 `"foo"`。
  - `modifiers`：一个包含修饰符的对象。例如：`v-my-directive.foo.bar` 中，修饰符对象为 `{ foo: true, bar: true }`。
- `oldVnode`：上一个虚拟节点，仅在 `update` 和 `componentUpdated` 钩子中可用。

![](https://cdn.nlark.com/yuque/0/2019/png/271124/1557981403487-88a67750-c0c9-41d7-9112-d52bdc8b3534.png#align=left&display=inline&height=142&originHeight=310&originWidth=1632&status=done&width=746)


