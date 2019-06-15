---
title: 14 连接redis
date: 2019-06-02 16:47:43
tags: egg-企业级框架和应用入门
desc: 
# keywords: 
categories:
  - egg-企业级框架和应用入门
# from: https://bitsofco.de/the-background-properties/
# demo: ../../../demos/201703/background.html
---

> Redis client(support redis portocal) based on ioredis for egg framework


### 14.1 安装

```bash
npm i egg-redis --save
```
<!--more-->
### 14.2 配置
Change `${app_root}/config/plugin.js` to enable redis plugin:

```javascript
exports.redis = {

  enable: true,

  package: 'egg-redis',

};
```


Configure redis information in `${app_root}/config/config.default.js`:<br />**Single Client**

```javascript
config.redis = {
  client: {
    port: 6379,          // Redis port
    host: '127.0.0.1',   // Redis host
    password: 'auth',
    db: 0,
  }
}
```

### 14.3 使用方法

#### []()14.3.1 service
app/service/redis.js
`if(this.app.redis)`判断是否有启用redis
```javascript
'use strict';

const Service = require('egg').Service;

class RedisService extends Service {
  async set(key, value, seconds) {
    value = JSON.stringify(value);
    if (this.app.redis) {
      if (!seconds) {
        await this.app.redis.set(key, value);
      } else {
        await this.app.redis.set(key, value, 'EX', seconds);
      }
    }
  }

  async get(key) {
    if (this.app.redis) {
      const data = await this.app.redis.get(key);
      if (!data) return;
      return JSON.parse(data);
    }
  }
}

module.exports = RedisService;

```

#### []()14.3.2 controller
app/controller/default/index.js如果没有设置redis缓存，就去请求数据,再设置缓存

```javascript
var topNav = await this.ctx.service.cache.get('index_topNav');
if (!topNav) {
  topNav = await this.ctx.model.Nav.find({
    "position": 1
  });
  await this.ctx.service.cache.set('index_topNav', topNav, 60 * 60);
}
```


