---
title: 11 全局api-set
date: 2019-05-15 21:10:04
tags: Vue基础入门笔记
# desc: 作用域就是变量的作用范围。也就是你声明一个变量以后，这个变量可以在什么场合下使用。以前的JavaScript只有全局作用域，和函数作用域。
# keywords: 
categories:
  - Vue基础入门笔记
# from: https://bitsofco.de/the-background-properties/
# demo: ../../../demos/201703/background.html
---

## 官网说明

Vue.set( target, propertyName/index, value )

- **参数**：
  - `{Object | Array} target`
  - `{string | number} propertyName/index`
  - `{any} value`
- **返回值**：设置的值。<br />
- **用法**：<br />向响应式对象中添加一个属性，并确保这个新属性同样是响应式的，且触发视图更新。它必须用于向响应式对象上添加新属性，因为 Vue 无法探测普通的新增属性 (比如 `this.myObject.newProperty = 'hi'`)

> 注意对象不能是 Vue 实例，或者 Vue 实例的根数据对象。<br />

## 示例

```javascript
<div id="div">  
	<p >{{items}}</p>
</div>
 
<script>
 
var vm = new Vue({
el:"#div",
  data: {
    items: ['a', 'b', 'c']
  }
});
 
Vue.set(vm.items,2,"ling")
 
</script>
```

<a name="oQmUK"></a>
### 1 设置数组元素

Vue.set(vm.items,2,"ling") : 表示 把vm.items  这个数组的下标为2 的元素，改为"ling"<br />把数组  ["a","b","c"] 修改 后是 ["a","b","ling"] <br />**<br />**![image.png](https://cdn.nlark.com/yuque/0/2019/png/271124/1560263719161-45ef7ee2-d80c-4e04-96ff-bb521da96e0b.png#align=left&display=inline&height=80&name=image.png&originHeight=160&originWidth=616&size=8949&status=done&width=308)**<br />**
<a name="ZGzgO"></a>
### 2 向响应式对象添加属性

```javascript
<div id="div">  
	<p>{{person}}</p>
</div>
 
<script>
var vm = new Vue({
el:"#div",
data: {
   person:{
			name:"ling",
			job:"engineer"
   }
},
created:function(){
		alert(this.person.age)
  }
});
 
Vue.set(vm.person,"age","26")
</script>
```

> 注意：person 是data 里面的子对象，所以可以使用 Vue.set( ) 方法。data 这个根对象就不能使用 set 方法



![image.png](https://cdn.nlark.com/yuque/0/2019/png/271124/1560264428484-2a01d752-cb52-453b-a2f5-86e7f23dc4e3.png#align=left&display=inline&height=122&name=image.png&originHeight=244&originWidth=916&size=42867&status=done&width=458)

![image.png](https://cdn.nlark.com/yuque/0/2019/png/271124/1560264440722-f7f3ac4b-49eb-478f-b980-70034bbe8687.png#align=left&display=inline&height=94&name=image.png&originHeight=188&originWidth=904&size=40740&status=done&width=452)

> **说明：控制台可以在person 里找到age 这个属性，说明添加成功 (响应式)**

**
<a name="tdJHQ"></a>
## 对比非响应式方法
**vm.food="chocolate"**<br />alert(vm.food)

![image.png](https://cdn.nlark.com/yuque/0/2019/png/271124/1560264596937-87d15eb3-16b3-4d5d-abd5-3dcf1358123f.png#align=left&display=inline&height=131&name=image.png&originHeight=262&originWidth=1400&size=42983&status=done&width=700)

> **控制台和网页上的 {{person}} 都没有显示food 这个属性，说明food 这个属性没有被添加 （非响应式）**

**<br />**![image.png](https://cdn.nlark.com/yuque/0/2019/png/271124/1560264665607-ec58d779-389f-4945-a269-e548d1e694b6.png#align=left&display=inline&height=374&name=image.png&originHeight=748&originWidth=1264&size=145380&status=done&width=632)**

