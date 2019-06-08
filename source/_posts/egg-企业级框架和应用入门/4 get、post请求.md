---
title: 4 get、post请求
date: 2019-06-01 13:47:43
tags: egg-企业级框架和应用入门
desc: 
# keywords: 
categories:
  - egg-企业级框架和应用入门
# from: https://bitsofco.de/the-background-properties/
# demo: ../../../demos/201703/background.html
---
### 4.1 get 请求
#### 4.1.1 query
在 URL 中 `?`后面的部分是一个 Query String，这一部分经常用于 GET 类型的请求中传递参数。例如 `GET /search?name=egg&age=26`中 `name=egg&age=26` 就是用户传递过来的参数。我们可以通过 `context.query`(为一个对象)拿到解析过后的这个参数体

```javascript
module.exports = app => {

class HomeController extends Controller {
  async getQuery() {
      const queryObj = this.ctx.query;
      console.log(queryObj.age);
      console.log(queryObj);
      //打印结果：{ name: 'egg', age: '26' }
    }
  }
  return SearchController;
};
```

<br />当 Query String 中的 key 重复时，`context.query`只取 key 第一次出现时的值，后面再出现的都会被忽略。`GET /posts?category=egg&category=koa` 通过 `context.query`拿到的值是 `{ category: 'egg' }`。
<a name="c1fd7d6c"></a>
#### 4.1.2   queries
有时候我们的系统会设计成让用户传递相同的 key，例如 `GET /posts?category=egg&id=1&id=2&id=3`。针对此类情况，框架提供了 `context.queries` 对象，这个对象也解析了 Query String，但是它不会丢弃任何一个重复的数据，而是将他们都放到一个`数组`中：<br />

```javascript
// GET /posts?category=egg&id=1&id=2&id=3
const Controller = require('egg').Controller;

class HomeController extends Controller {
  async getQueries() {
    console.log(this.ctx.queries);
    //result:
    // {
    //   category: [ 'egg' ],
    //   id: [ '1', '2', '3' ],
    // }
  }
};
```

`context.queries`上所有的 key 如果有值，也一定会是`数组`类型。

<a name="0031db38"></a>
### 4.2 post 请求

```javascript
// 获取参数方法 post 请求


module.exports = app => {
class HomeController extends Controller {
  async postObj() {
      const queryObj = ctx.request.body;
      ctx.body = queryObj;
    }
  }
  return SearchController;
};
```

---

> 但是我们请求有时是get,有时是post,有时本来应该是post的请求,但是为了测试方便,还是做成get和post请求都支持的请求,于是一个能同时获取get和post请求参数的中间件就很有必要了.


<a name="8c221a17"></a>
### 4.3 编写中间层解决get、post请求
<a name="2b154e51"></a>
#### 4.3.1 在app目录下新建middleware文件夹
<a name="71a0e970"></a>
#### 4.3.2 在middleware里面新建params.js,内容如下

```javascript
/**
 * 获取请求参数中间件
 * 可以使用ctx.params获取get或post请求参数
 */
module.exports = options => {
  return async function params(ctx, next) {
    ctx.params = {
      ...ctx.query,
      ...ctx.request.body
    }
    await next();
  };
};
```
本质上就是把get请求的参数和post请求的参数都放到params这个对象里,所以,不管是get还是post都能获取到请求参数

<a name="c127c48b"></a>
#### 4.3.3 在/config/config.default.js里注入中间件

```javascript
'use strict';
module.exports = appInfo => {
  const config = exports = {};
// 注入中间件
  config.middleware = [
    'params',
  ];
  return config;
};
```

<a name="cf8dc011"></a>
#### 4.3.4 使用文章获取

```javascript
/**
 * 添加文章接口
 */
'use strict';
const Service = require('egg').Service;
class ArticleService extends Service {
  async add() {
    const { ctx } = this;
    // 获取请求参数
    const {
      userId,
      title,
      content,
    } = ctx.params;
    const result = await ctx.model.Article.create({
      userId,
      title,
      content,
    });
    return result;
  }
}
module.exports = ArticleService;
```

<a name="1a577bcd"></a>
### 4.3 允许post请求跨域 

```javascript
// config/plugin.js
exports.cors = {
  enable: true,
  package: 'egg-cors',
};
```

```javascript
 // config/config.default.js
config.security = {
  csrf: {
    enable: false,
    ignoreJSON: true,
  },
  domainWhiteList: [ 'http://www.baidu.com' ], // 配置白名单
};

config.cors = {
  // origin: '*',//允许所有跨域访问，注释掉则允许上面 白名单 访问
  allowMethods: 'GET,HEAD,PUT,POST,DELETE,PATCH',
};
```

*一般性最好使用白名单，不要使用全部允许跨域，不安全
