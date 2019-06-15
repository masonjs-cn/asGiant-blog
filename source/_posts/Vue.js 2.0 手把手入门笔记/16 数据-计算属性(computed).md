---
title: 16 数据-计算属性(computed)
date: 2019-05-16 13:10:04
tags: Vue基础入门笔记
# desc: 作用域就是变量的作用范围。也就是你声明一个变量以后，这个变量可以在什么场合下使用。以前的JavaScript只有全局作用域，和函数作用域。
# keywords: 
categories:
  - Vue基础入门笔记
# from: https://bitsofco.de/the-background-properties/
# demo: ../../../demos/201703/background.html
---

### 9.1 什么是计算属性
模板内的表达式非常便利，但是设计它们的初衷是用于**简单运算的**。在模板中放入太多的逻辑会让模板过重且难以维护。例如:
```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title>vue</title>
</head>
<body>
    <div id="app">
       <div id="example">
           {{ message.split('').reverse().join('') }}
       </div>
    </div>
</body>
<script src="https://cdn.jsdelivr.net/npm/vue"></script> 
<script>
    var vm = new Vue({
      el: '#app',
      data: {
        message: 'Hello'
      }
    });
  </script>
  </div>

</html>
```

![image.png](https://cdn.nlark.com/yuque/0/2019/png/271124/1557891066357-d1d57de9-4042-4703-9111-b54d669c4515.png#align=left&display=inline&height=35&name=image.png&originHeight=70&originWidth=162&size=1943&status=done&width=81)

这里的表达式包含3个操作，并不是很清晰，所以遇到复杂逻辑时应该使用Vue特带的计算属性computed来进行处理。

<a name="4xZcY"></a>
### 9.2 计算属性的用法

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title>vue</title>
</head>
<body>
    <div id="app">
       <div id="example">
           {{getMessage}}
       </div>
    </div>
</body>
<script src="https://cdn.jsdelivr.net/npm/vue"></script> 
<script>
    var vm = new Vue({
      el: '#app',
      data: {
        message: 'Hello'
      },
      computed: { // 放在computed中最后也会放在vm上，不能和methods与data重名
        getMessage() {
            return this.message.split('').reverse().join('')
        }
      }
    });
  </script>
  </div>

</html>
```

<a name="uNF1P"></a>
### 9.3 计算属性使用技巧
计算属性可以依赖其他计算属性<br />计算属性不仅可以依赖当前Vue 实例的数据，还可以依赖其他实例的数据

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title>vue</title>
</head>
<body>
    <div id="app1"></div>
    <div id="app2">
         {{getMessage}}
    </div>
</body>
<script src="https://cdn.jsdelivr.net/npm/vue"></script> 
<script>
    var vm= new Vue({
      el: '#app1',
      data: {
        message: 'World'
      }
    });
    var vm2 = new Vue({
      el: '#app2',
      data: {
        message: 'Hello'
      },
      computed: { 
        getMessage() {
            return `${this.message} ${vm.message}`
        }
      }
    });
  </script>
  </div>
</html>
```

<a name="4EDMS"></a>
### 9.4 getter和setter
每一个计算属性都包含一个getter 和一个setter ，我们上面的两个示例都是计算属性的默认用法， 只是利用了getter 来读取。<br />在你需要时，也可以提供一个setter 函数， 当手动修改计算属性的值就像修改一个普通数据那样时，就会触发setter 函数，执行一些自定义的操作

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title>vue</title>
</head>
<body>
    <div id="app">
        <input type="text" v-model="getMessage"> <--模拟修改--!>
        {{getMessage}}
    </div>
</body>
<script src="https://cdn.jsdelivr.net/npm/vue"></script> 
<script>
    var vm= new Vue({
      el: '#app',
      data: {
        hi:'Hello',
        message: 'World'
      },
      computed:{
        getMessage:{ //get,set方法
           // getter
           get(){
             return this.hi + ' ' + this.message
           },
           // setter
           set(newValue){
              console.log('====================================');
              console.log(newValue);
              console.log('====================================');
              var names = newValue.split(' ');
              this.hi = names[0];
              this.message = names[names.length - 1];
           }
        }
      }
    });
  </script>
</html>
```

<br />绝大多数情况下，我们只会用默认的getter 方法来读取一个计算属性，在业务中很少用到setter,所以在声明一个计算属性时，可以直接使用默认的写法，不必将getter 和setter 都声明。

<a name="ID8m7"></a>
### 9.5 质疑什么不直接用methods
我们可以将同一函数定义为一个方法而不是一个计算属性，两种方式的最终结果确实是完全相同的。只是一个使用getMessage()取值，一个使用getMessage取值。<br />然而，不同的是**计算属性是基于它们的依赖进行缓存的**。计算属性只有在它的相关依赖发生改变时才会重新求值。<br />这就意味着只要 hi还没有发生改变，多次访问 getMessage计算属性会立即返回之前的计算结果，而不必再次执行函数。

```javascript
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title>vue</title>
</head>
<body>
    <div id="app">
        <div>{{getMessage}}</div>
        <div> {{getMessage1()}}</div>
    </div>
</body>
<script src="https://cdn.jsdelivr.net/npm/vue"></script> 
<script>
    var vm= new Vue({
      el: '#app',
      data: {
        hi:'Hello',
        message: 'World'
      },
      computed:{
        getMessage(){ //get,set方法
            return this.hi + ' ' + this.message 
            //而使用计算属性，只要title没变，页面渲染是不会重新进这里来计算的，而是使用了缓存。
        }
      },
      methods:{
        getMessage1(){
            return this.hi + ' ' + this.message
            //进这个方法，再次计算。不是刷新，而是只要页面渲染，就会进方法里重新计算。
        }
      }
    });
  </script>
</html>
```

