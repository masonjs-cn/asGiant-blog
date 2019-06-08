---
title: 6 Cookie 的使用
date: 2019-06-01 15:47:43
tags: egg-企业级框架和应用入门
desc: 
# keywords: 
categories:
  - egg-企业级框架和应用入门
# from: https://bitsofco.de/the-background-properties/
# demo: ../../../demos/201703/background.html
---

# 6 Cookie 的使用

<a name="8e2bda97"></a>
### 6.1 Cookie 简介
- cookie 是存储于访问者的计算机中的变量。可以让我们用同一个浏览器访问同一个域名的时候共享数据。
- HTTP 是无状态协议。简单地说，当你浏览了一个页面，然后转到同一个网站的另一个页面，服务器无法认识到这是同一个浏览器在访问同一个网站。每一次的访问，都是没有任何关系的。

<a name="e8c79d52"></a>
### 6.2 Cookie 的设置和获取

<a name="3a998b31"></a>
#### 6.2.1 Cookie 设置语法
> ctx.cookies.set(key, value, options)


```javascript
this.ctx.cookies.set('name','zhangsan');
```

<a name="4fe3e7c9"></a>
#### 6.2.2 Cookie 获取语法
> ctx.cookies.get(key, options)


```javascript
this.ctx.cookies.get('name')
```


<a name="fc196a74"></a>
#### 6.2.3 清除 Cookie

```javascript
this.ctx.cookies.set('name',null);
```

或者设置 maxAge 过期时间为 0

<a name="1f376170"></a>
### 6.3 Cookie 参数 options
>  https://eggjs.org/en/core/cookie-and-session.html#container


```javascript
ctx.cookies.set(key, value, {
  maxAge:24 * 3600 * 1000,
  httpOnly: true, // 默认情况下是正确的
  encrypt: true, // cookie在网络传输期间加密
  ctx.cookies.get('frontend-cookie', {
  encrypt: true
});
```
<a name="d41d8cd9"></a>
### 
<a name="95f56a9e"></a>
### 6.4 设置中文 Cookie
<a name="04aae555"></a>
#### 6.4.1 第一种解决方案

```javascript
console.log(new Buffer('hello, world!').toString('base64'));
// 转换成 base64字符串：aGVsbG8sIHdvcmxkIQ==
console.log(new Buffer('aGVsbG8sIHdvcmxkIQ==', 'base64').toString()); // 还原 base64字符串：hello, world!
```

<a name="06fdf631"></a>
#### 6.4.2 第二种解决方案

```javascript
ctx.cookies.set(key, value, {
	maxAge:24 * 3600 * 1000,
	httpOnly: true, // 默认情况下是正确的
	encrypt: true, // cookie在网络传输期间进行加密
});
```


