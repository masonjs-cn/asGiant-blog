---
title: 17 数据-观察(watch)
date: 2019-05-16 14:10:04
tags: Vue基础入门笔记
# desc: 作用域就是变量的作用范围。也就是你声明一个变量以后，这个变量可以在什么场合下使用。以前的JavaScript只有全局作用域，和函数作用域。
# keywords: 
categories:
  - Vue基础入门笔记
# from: https://bitsofco.de/the-background-properties/
# demo: ../../../demos/201703/background.html
---


一个对象，键是需要观察的表达式，值是对应回调函数。值也可以是方法名，或者包含选项的对象。Vue 实例将会在实例化时调用 `$watch()`，遍历 watch 对象的每一个属性。
> 为什么一定要有watch，不用可以吗？我们已经有了computed，能不能不去使用?

<a name="CHjff"></a>
## 1 watch的出现
> 做一个实验

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title>vue</title>
</head>
<body>
    <div id="app">
        <input type="text" v-model="a">
    </div>
</body>
<script src="https://cdn.jsdelivr.net/npm/vue"></script> 
<script>

    var vm = new Vue({
        el:'#app',
        data:{
            a:"1"
        },
        computed: {
            a(){
               setTimeout(() => {
                   this.a=1;
               }, 500); 
            }
        }
    })
</script>
</html>
```

> 不难发现在_异步的情况下就不好使用了_

<a name="dEza4"></a>
## 2 代码实现
```javascript
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title>vue</title>
</head>
<body>
    <div id="app">
        <input type="text" v-model="a">
    </div>
</body>
<script src="https://cdn.jsdelivr.net/npm/vue"></script> 
<script>
    var vm = new Vue({
        el:'#app',
        data:{
            a:""
        },
        watch: { // 只有值变化的时候才会触发 支持异步了，其他情况我们更善于使用
            a(newVal,oldVal){ // watch的属性名字要和观察的人的名字一致
                console.log(newVal);
                console.log(oldVal);
            }
        },
    })
</script>
</html>
```

<a name="ofjYE"></a>
## 3 computed与watch的区别
Vue 提供了一种更通用的方式来观察和响应 Vue 实例上的数据变动:**侦听属性**。当你有一些数据需要随着其它数据变动而变动时，你很容易滥用 `watch`

```javascript
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title>vue</title>
</head>
<body>
    <div id="app">
        {{ fullName }}
    </div>
</body>
<script src="https://cdn.jsdelivr.net/npm/vue"></script> 
</html>
```

```javascript
    var vm = new Vue({
    el: '#app',
        data: {
            firstName: 'Foo',
            lastName: 'Bar',
            fullName: 'Foo Bar'
        },
        watch: {
            firstName: function (val) {
                this.fullName = val + ' ' + this.lastName
            },
            lastName: function (val) {
                this.fullName = this.firstName + ' ' + val
            }
        }
    })
```

上面代码是命令式且重复的。将它与计算属性的版本进行比较：

```javascript
var vm = new Vue({
  el: '#demo',
  data: {
    firstName: 'Foo',
    lastName: 'Bar'
  },
  computed: {
    fullName: function () {
      return this.firstName + ' ' + this.lastName
    }
  }
})
```

> 是不是感觉优雅很多


<a name="FM8YE"></a>
## 4 侦听器
虽然计算属性在大多数情况下更合适，但有时也需要一个自定义的侦听器。这就是为什么 Vue 通过 watch 选项提供了一个更通用的方法，来响应数据的变化。当需要在数据变化时执行异步或开销较大的操作时，这个方式是最有用的。

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title>vue</title>
</head>
<body>
    <div id="app">
       <input type="text" v-model="something">
       {{somethingShow}}
    </div>
</body>
<script src="https://cdn.jsdelivr.net/npm/vue"></script> 
<script>
    var vm = new Vue({
    el: '#app',
        data: {
            something: '',
            somethingShow:''
        },
        watch: {
            something(val){
                this.somethingShow = "loading"
                this.getSomething()
            }
        },
        methods:{
            getSomething(){
                setTimeout(() => {
                    this.somethingShow = "hello"
                }, 1000);// 我们使用延迟模拟一个网络请求
            }
        }
    })
</script>
</html>
```

<a name="uY7RX"></a>
## 5 vm.$watch
> vm.$watch( expOrFn, callback, [options] )

观察 Vue 实例变化的一个表达式或计算属性函数。回调函数得到的参数为新值和旧值。表达式只接受监督的键路径。对于更复杂的表达式，用一个函数取代。

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title>vue</title>
</head>
<body>
    <div id="app">
       <input type="text" v-model="something">
       {{somethingShow}}
    </div>
</body>
<script src="https://cdn.jsdelivr.net/npm/vue"></script> 
<script>
    var vm = new Vue({
    el: '#app',
        data: {
            something: '',
            somethingShow:''
        }
    })
    vm.$watch('something',(newVal,oldVal)=>{// watch的属性名要和观察的人名字一致
        vm.somethingShow = "loading"
        console.log('====================================');
        console.log(newVal);
        console.log('====================================');
        vm.somethingShow = newVal
    })
</script>
</html>
```

