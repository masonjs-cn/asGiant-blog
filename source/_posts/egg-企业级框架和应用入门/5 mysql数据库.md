---
title: 5 mysql数据库
date: 2019-06-01 14:47:43
tags: egg-企业级框架和应用入门
desc: 
# keywords: 
categories:
  - egg-企业级框架和应用入门
# from: https://bitsofco.de/the-background-properties/
# demo: ../../../demos/201703/background.html
---

# 5 mysql数据库

框架提供了 egg-mysql 插件来访问 MySQL 数据库。这个插件既可以访问普通的 MySQL 数据库，也可以访问基于 MySQL 协议的在线数据库服务。<br />

<a name="41f4681f"></a>
### [](https://eggjs.org/zh-cn/tutorials/mysql.html#%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE)5.1 安装与配置
安装对应的插件 egg-mysql :

```javascript
npm i --save egg-mysql
```

开启插件：

```javascript
// config/plugin.js
exports.mysql = {
  enable: true,
  package: 'egg-mysql',
};
```

在 `config/config.${env}.js` 配置各个环境的数据库连接信息。

<a name="b76e9b5d"></a>
#### [](https://eggjs.org/zh-cn/tutorials/mysql.html#%E5%8D%95%E6%95%B0%E6%8D%AE%E6%BA%90)5.1.1 单数据源
如果我们的应用只需要访问一个 MySQL 数据库实例，可以如下配置：<br />使用方式：

```javascript
// config/config.${env}.js
exports.mysql = {
  // 单数据库信息配置
  client: {
    // host
    host: 'mysql.com',
    // 端口号
    port: '3306',
    // 用户名
    user: 'test_user',
    // 密码
    password: 'test_password',
    // 数据库名
    database: 'test',
  },
  // 是否加载到 app 上，默认开启
  app: true,
  // 是否加载到 agent 上，默认关闭
  agent: false,
};
```

```javascript
await app.mysql.query(sql, values); // 单实例可以直接通过 app.mysql 访问
```

<a name="f0cdea86"></a>
#### [](https://eggjs.org/zh-cn/tutorials/mysql.html#%E5%A4%9A%E6%95%B0%E6%8D%AE%E6%BA%90)5.1.2 多数据源
如果我们的应用需要访问多个 MySQL 数据源，可以按照如下配置：

```javascript
exports.mysql = {
  clients: {
    // clientId, 获取client实例，需要通过 app.mysql.get('clientId') 获取
    db1: {
      // host
      host: 'mysql.com',
      // 端口号
      port: '3306',
      // 用户名
      user: 'test_user',
      // 密码
      password: 'test_password',
      // 数据库名
      database: 'test',
    },
    db2: {
      // host
      host: 'mysql2.com',
      // 端口号
      port: '3307',
      // 用户名
      user: 'test_user',
      // 密码
      password: 'test_password',
      // 数据库名
      database: 'test',
    },
    // ...
  },
  // 所有数据库配置的默认值
  default: {
  },
  // 是否加载到 app 上，默认开启
  app: true,
  // 是否加载到 agent 上，默认关闭
  agent: false,
};
```

<a name="0c420b74"></a>
### 5.2 封装增删改查
<a name="a70fb78d"></a>
#### 5.2.1、插入，向users表内插入一条数据

```javascript
const result = await this.app.mysql.insert('users', {
    name: 'wjw',
    age: 18
  })
// 判断：result.affectedRows === 1
```

<a name="8aec9d6f"></a>
#### 5.2.2、查询，查询users表name=Jack的数据

```javascript
const result = await this.app.mysql.select('users', {
    columns: ['id', 'name'], //查询字段，全部查询则不写，相当于查询*
    where: {
        name: 'wjw'
    }, //查询条件
    orders: [
        ['id', 'desc'] //降序desc，升序asc
    ],
    limit: 10, //查询条数
    offset: 0 //数据偏移量（分页查询使用）
  })
//判断：result.length > 0
```

<a name="b83f1814"></a>
#### 5.2.3、修改，修改users表id=1的数据age为20

```javascript
const result = await this.app.mysql.update('users', {
      age: 20 //需要修改的数据
  }, {
      where: {
        id: 1
      } //修改查询条件
  });
//判断：result.affectedRows === 1
```

<a name="9a47efed"></a>
#### 5.2.4、删除，删除users表name=wjw的数据

```javascript
const result = await this.app.mysql.delete('users', {
    name: 'wjw'
})
```

