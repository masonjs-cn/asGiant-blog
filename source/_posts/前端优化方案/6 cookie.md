---
title: 6 cookie
date: 2019-04-15 17:10:04
tags: 前端优化方案
desc: 
# keywords: 
categories:
  - 前端优化方案
# from: https://bitsofco.de/the-background-properties/
# demo: ../../../demos/201703/background.html
---

### 6.1 给Cookie减肥
使用cookie的原因有很多，比如授权和个性化。HTTP头中cookie信息在web服务器和浏览器之间交换。重要的是保证cookie尽可能的小，以最小化对用户响应时间的影响。

- 清除不必要的cookie
- 保证cookie尽可能小，以最小化对用户响应时间的影响
- 注意给cookie设置合适的域级别，以免影响其它子域
- 设置合适的有效期，更早的有效期或者none可以更快的删除cookie，提高用户响应时间

<a name="42ef8014"></a>
### 6.2 把组件放在不含cookie的域下
当浏览器发送对静态图像的请求时，cookie也会一起发送，而服务器根本不需要这些cookie。所以它们只会造成没有意义的网络通信量，应该确保对静态组件的请求不含cookie。可以创建一个子域，把所有的静态组件都部署在那儿。<br />如果域名是www.example.org，可以把静态组件部署到static.example.org。然而，如果已经在顶级域example.org或者www.example.org设置了cookie，那么所有对static.example.org的请求都会含有这些cookie。这时候可以再买一个新域名，把所有的静态组件部署上去，并保持这个新域名不含cookie。Yahoo!用的是yimg.com，YouTube是ytimg.com，Amazon是images-amazon.com等等。<br /> 把静态组件部署在不含cookie的域下还有一个好处是有些代理可能会拒绝缓存带cookie的组件。有一点需要注意：如果不知道应该用example.org还是www.example.org作为主页，可以考虑一下cookie的影响。省略www的话，就只能把cookie写到*.example.org，所以因为性能原因最好用www子域，并且把cookie写到这个子域下。
