---
title: 4 egg-mongoose 配置
date: 2019-04-10 11:10:04
tags: mongoose
desc: 
# keywords: 
categories:
  - mongoose
# from: https://bitsofco.de/the-background-properties/
# demo: ../../../demos/201703/background.html
---
### 4.1 安装

```
$ npm install egg-mongoose --save
```

<a name="Wmyad"></a>
### 4.2 配置
> 改变Egg项目中的配置文件{workplace}/config/plugin.js中来启用 egg-mongoose 插件:


```
exports.mongoose = {
  enable: true,
  package: 'egg-mongoose',
};
```
<a name="OpgPS"></a>
## 
<a name="xrnpV"></a>
### 4.3 Egg连接mongoose
> 在Egg项目中的配置文件{workplace}/config/default.js配置项config添加属性


```javascript
config.mongoose = {
    url: process.env.EGG_MONGODB_URL || 'mongodb://127.0.0.1/website',
    options: {
      server: {
        poolSize: 40,
      },
    },
  };
```


> 连接方法


```javascript
 config.mongoose = {
    client: {
      url: 'mongodb://账号:密码@服务器:端口/库名',
      options: {},
    },
  };
```

