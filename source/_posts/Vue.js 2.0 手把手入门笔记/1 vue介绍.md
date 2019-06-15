---
title: 1 vue介绍
date: 2019-05-15 11:10:04
tags: Vue基础入门笔记
# desc: 作用域就是变量的作用范围。也就是你声明一个变量以后，这个变量可以在什么场合下使用。以前的JavaScript只有全局作用域，和函数作用域。
# keywords: 
categories:
  - Vue基础入门笔记
# from: https://bitsofco.de/the-background-properties/
# demo: ../../../demos/201703/background.html
---

### 1 介绍
> 是一套用于构建用户界面的渐进式框架。与其它大型框架不同的是，Vue 被设计为可以自底向上逐层应用。Vue 的核心库只关注视图层，不仅易于上手，还便于与第三方库或既有项目整合。


<a name="fGMqx"></a>
### 2 特点:

- 核心只关注视图层(view)
- 灵活、轻量、灵活的特点
- 适用于移动端项目
- 渐进式框架

<a name="bSkNB"></a>
### 3 什么是库，什么是框架？

- 库是将代码集合成一个产品，库是我们调用库中的方法实现自己的功能
- 框架则是为解决一类问题而开发的产品，框架是我们在指定的位置编写代码，框架帮我们调用。

> 框架是库的升级版


<a name="vWDCy"></a>
### 4 渐进式

- 声明式渲染(无需关心如何实现)
- 组件系统
- 客户端路由(vue-router)
- 大规模状态管理(vuex)
- 构建工具(vue-cli)

<a name="VD6t3"></a>
### 5 Vue的两个核心点

1. 响应的数据变化
  1. 当数据发生改变->视图的自动更新
2. 组合的视图组件
  1. ui页面映射为组件树
  1. 划分组件可维护、可复用、可测试
<a name="GHpTU"></a>
### 
<a name="NjiBB"></a>
### 6 MVC(backbone,react)

- model 数据
- view  视图
- controller 控制器

<a name="Ze24R"></a>
### 7 MVVM(angular,vue) 双向

- model 数据
- view  视图
- viewModel视图模型

<a name="xOTe8"></a>
### 8 Object.defineProperty(es5)没有替代方案 

- 不支持ie8<=
