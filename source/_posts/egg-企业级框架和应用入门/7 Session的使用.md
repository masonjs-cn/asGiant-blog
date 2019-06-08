---
title: 7 Session的使用
date: 2019-06-01 16:47:43
tags: egg-企业级框架和应用入门
desc: 
# keywords: 
categories:
  - egg-企业级框架和应用入门
# from: https://bitsofco.de/the-background-properties/
# demo: ../../../demos/201703/background.html
---
### 7.1 Session 简单介绍
session 是另一种记录客户状态的机制，不同的是 Cookie 保存在客户端浏览器中，而session 保存在服务器上。<br />

<a name="c48ea833"></a>
### 7.2 Session 的工作流程
当浏览器访问服务器并发送第一次请求时，服务器端会创建一个 session 对象，生成一个类似于 key,value 的键值对， 然后将 key(cookie)返回到浏览器(客户)端，浏览器下次再访问时，携带 key(cookie)，找到对应的 session(value)。

<a name="f6c72f68"></a>
### 7.3 Egg.js 中 session 的使用
egg.js 中 session 基于 egg-session 内置了对 session 的操作<br />

<a name="19d42806"></a>
#### 7.3.1 设置

```javascript
this.ctx.session.userinfo={
	name:'张三', 
  age:'20'
}
```

<a name="04e49ebc"></a>
#### 7.3.2 获取

```javascript
var userinfo=this.ctx.session
```

<a name="23e6b3cc"></a>
#### 7.3.3 Session 的默认设置

```javascript
exports.session = {
  key: 'EGG_SESS',
  maxAge: 24 * 3600 * 1000, // 1 day httpOnly: true,
  encrypt: true
};
```

<a name="1bc23133"></a>
### 7.4 Session 在 config.default.js 中的配置

```javascript
config.session={
  key:'SESSION_ID',
  maxAge:864000,
  renew: true //延长会话有效期
}
```

<a name="b5b6978f"></a>
### 7.5 cookie 和session 区别

- cookie 数据存放在客户的浏览器上，session 数据放在服务器上。
- cookie 相比 session 没有 session 安全，别人可以分析存放在本地的 COOKIE 并进行 COOKIE欺骗。
- session 会在一定时间内保存在服务器上。当访问增多，会比较占用你服务器的性能考虑到减轻服务器性能方面，应当使用 COOKIE。
- 单个 cookie 保存的数据不能超过 4K，很多浏览器都限制一个站点最多保存 20 个 cookie。
