---
title: 4 数组的循环v-for
date: 2019-05-15 14:10:04
tags: Vue基础入门笔记
# desc: 作用域就是变量的作用范围。也就是你声明一个变量以后，这个变量可以在什么场合下使用。以前的JavaScript只有全局作用域，和函数作用域。
# keywords: 
categories:
  - Vue基础入门笔记
# from: https://bitsofco.de/the-background-properties/
# demo: ../../../demos/201703/background.html
---

> vue 提供了一个v-for 解决循环问题 更高效 会复用原有结构

## 4.1 代码
```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title>vue</title>
</head>
<body>
    <div id="content">
        <!--要循环谁就在谁身上增加v-for属性,类似于for...in..-->
        <!--默认是value of 数组/ (value,index) of 数组-->
        <li v-for="(todo,index) in todos">
 <!-- 会改变原始数组的方法，为变异方法 例如push(),pop()等；  非变异方法，不会改变原始数组，但是会返回一个新数组 -->
            {{ todo.text }} {{index+1}}
        </li>
    </div>
</body>
<script src="https://cdn.jsdelivr.net/npm/vue"></script> 
<!-- 使用官网的vue地址 -->
<script>
    let vm = new Vue({
        el:'#content',
        data:{
            todos: [
                { text: '学习 JavaScript' },
                { text: '学习 Vue' },
                { text: '整个牛项目' }
            ]
        }
    })
</script>
</html>
```

v-for循环数组 当用for来更新已被渲染的元素时，vue的“就地复用”机制 是不会改变数据项的顺序的。要想重新排序，需为每项添加key属性（也就是每项唯一的id）
> 想要改变

会改变原始数组的方法，为变异方法 例如push(),pop()等；  非变异方法，不会改变原始数组，但是会返回一个新数组

## 4.2 为什么v-for一定要有key

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title>vue</title>
</head>
<body>
    <div id="app">
        <div>
            <input type="text" v-model="name">
            <button @click="add">添加</button>
        </div>
        <ul>
            <li v-for="(item, i) in list">
                <input type="checkbox"> {{item.name}}
            </li>
        </ul>
    </div>
</body>
<script src="https://cdn.jsdelivr.net/npm/vue"></script> 
<!-- 使用官网的vue地址 -->
<script>
    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {
        name: '',
        newId: 3,
        list: [
          { id: 1, name: '蔬菜' },
          { id: 2, name: '奶酪' },
          { id: 3, name: '肉' }
        ]
      },
      methods: {
        add() {
         //注意这里是unshift
          this.list.unshift({ id: ++this.newId, name: this.name })
          this.name = ''
        }
      }
    });
  </script>
  </div>

</html>
```

![image.png](https://cdn.nlark.com/yuque/0/2019/png/271124/1557848419774-252c5099-6dab-4351-b4c8-0f421d329738.png#align=left&display=inline&height=124&name=image.png&originHeight=248&originWidth=452&size=14182&status=done&width=226)

当你输入汤时

![image.png](https://cdn.nlark.com/yuque/0/2019/png/271124/1557848450787-196c3b5c-0dce-43e3-b6d9-d1fb8025790f.png#align=left&display=inline&height=117&name=image.png&originHeight=234&originWidth=396&size=14428&status=done&width=198)

就会变成这个样子  => 

![image.png](https://cdn.nlark.com/yuque/0/2019/png/271124/1557848474048-a6753a52-c13d-4159-9079-5b9e2ab01419.png#align=left&display=inline&height=146&name=image.png&originHeight=292&originWidth=436&size=41906&status=done&width=218)
> 但是当你换成了key


> 可以简单的这样理解：加了key(一定要具有唯一性) id的checkbox跟内容进行了一个关联。是我们想达到的效果 


vue和react的虚拟DOM的Diff算法大致相同，其核心是基于两个简单的假设<br />首先讲一下diff算法的处理方法，对操作前后的dom树同一层的节点进行对比，一层一层对比，如下图：

![image.png](https://cdn.nlark.com/yuque/0/2019/png/271124/1557848744900-ea161cb7-2389-4531-b837-f973dfb63e0c.png#align=left&display=inline&height=318&name=image.png&originHeight=318&originWidth=576&size=40043&status=done&width=576)<br />当某一层有很多相同的节点时，也就是列表节点时，Diff算法的更新过程默认情况下也是遵循以上原则。<br />比如一下这个情况：<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/271124/1557848773830-6c12c8a7-8fb7-40f5-845f-155e6db6fa00.png#align=left&display=inline&height=191&name=image.png&originHeight=191&originWidth=477&size=32966&status=done&width=477)<br />我们希望可以在B和C之间加一个F，Diff算法默认执行起来是这样的：<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/271124/1557848802730-b07a12c6-76f3-4ea1-9175-0031d6b206f2.png#align=left&display=inline&height=215&name=image.png&originHeight=215&originWidth=572&size=54921&status=done&width=572)

即把C更新成F，D更新成C，E更新成D，最后再插入E，是不是很没有效率？<br />所以我们需要使用key来给每个节点做一个唯一标识，Diff算法就可以正确的识别此节点，找到正确的位置区插入新的节点。<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/271124/1557848842519-638c879e-7617-4697-9b8a-3d87dfacc524.png#align=left&display=inline&height=130&name=image.png&originHeight=130&originWidth=452&size=43650&status=done&width=452)

vue中列表循环需加:key="唯一标识" 唯一标识可以是item里面id index等，因为vue组件高度复用增加Key可以标识组件的唯一性，为了更好地区别各个组件 key的作用主要是为了高效的更新虚拟DOM



