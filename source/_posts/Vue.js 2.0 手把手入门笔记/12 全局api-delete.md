---
title: 12 全局api-delete
date: 2019-05-15 22:10:04
tags: Vue基础入门笔记
# desc: 作用域就是变量的作用范围。也就是你声明一个变量以后，这个变量可以在什么场合下使用。以前的JavaScript只有全局作用域，和函数作用域。
# keywords: 
categories:
  - Vue基础入门笔记
# from: https://bitsofco.de/the-background-properties/
# demo: ../../../demos/201703/background.html
---

Vue.delete( target, propertyName/index )

- **参数**：
  - `{Object | Array} target`
  - `{string | number} propertyName/index`
> 仅在 2.2.0+ 版本中支持 Array + index 用法。

- **用法**：<br />删除对象的属性。如果对象是响应式的，确保删除能触发更新视图。这个方法主要用于避开 Vue 不能检测到属性被删除的限制，但是你应该很少会使用它。
> 在 2.2.0+ 中同样支持在数组上工作。

- 目标对象不能是一个 Vue 实例或 Vue 实例的根数据对象。

```javascript
data:{
   namelist : {
     id : 1, 
       name : '叶落森'
   }       
}
```

```javascript
// 删除name
delete this.namelist.name;//js方法
Vue.delete(this.namelist,'name');//vue方法
```

