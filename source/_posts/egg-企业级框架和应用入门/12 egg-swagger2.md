---
title: 12 egg-swagger2
date: 2019-06-02 14:47:43
tags: egg-企业级框架和应用入门
desc: 
# keywords: 
categories:
  - egg-企业级框架和应用入门
# from: https://bitsofco.de/the-background-properties/
# demo: ../../../demos/201703/background.html
---
### 12.1 运营场景
作为后台,例如有人需要后台提供文档....人家java都有swagger,egg在 egg-swagger2 支持下，我们也可以使用。

<a name="Xcz0P"></a>
### 12.2 安装
> npm i egg-swagger2 -S

<a name="D7aau"></a>
### 12.3 开启插件

```javascript
// config/plugin.js
exports.swagger2 = {
  enable: true,
  package: 'egg-swagger2',
};
```

<a name="1gtoA"></a>
### 12.4 插件配置

config.default.js 中配置

```javascript
 config.swagger2 = {
    enable: true, // 禁用swagger , 默认为true
    base: {
      /* default config,support cover
      schemes: [
          'http',
      ],
      host: '127.0.0.1:7001',
      basePath: '/',
      consumes: [
      'application/json',
      ],
      produces: [
      'application/json',
      ],
      */
      info: {
        description: '文档介绍,
        version: '1.0.0',
        title: '文档名称',
        contact: {
          email: 'caandoll@aliyun.com',
        },
        license: {
          name: 'Apache 2.0',
          url: 'http://www.apache.org/licenses/LICENSE-2.0.html',
        },
      },
      tags: [{
          name: 'admin',
          description: 'Admin desc',
        },
        {
          name: 'role',
          description: 'Role desc',
        },
      ],
      definitions: {
        // model definitions
      },
      securityDefinitions: {
        // security definitions
      }
    },
  };
```

<a name="KfZ8e"></a>
### 12.4 例子
在  /app/router.js文件中
<a name="uZ8eN"></a>
#### 12.4.1 post请求
```javascript
module.exports = app => {
   const { router, controller, swagger } = app;
   router.post('/login', controller.test.postLogin);
   swagger.post('/login', {
       tags: [
         'admin',
       ],
       summary: 'Login a admin',
       description: '',
       parameters: [
         {
           in: 'body',
           name: 'body',
           description: 'admin\'s username & password',
           required: true,
           schema: {
             type: 'object',
             required: [ 'username', 'password' ],
             properties: {
               username: {
                 type: 'string',
                 description: 'admin\'s username',
               },
               password: {
                 type: 'string',
                 description: 'admin\'s password',
               },
             },
           },
         },
       ],
       responses: {
         200: {
           description: 'SUCCEED',
           schema: {
             type: 'object',
             properties: {
               status: {
                 type: 'string',
                 description: 'status',
               },
               data: {
                 type: 'object',
                 description: 'data',
                 properties: {
                   token: {
                     type: 'string',
                     description: 'token',
                   },
                 },
               },
             },
           },
         },
       },
     });
}
```

<a name="7CN29"></a>
#### 12.4.2 get请求

```javascript
module.exports = app => {
   const { router, controller, swagger } = app;
   router.get('/roles', controller.test.getRoles);
   swagger.get('/roles', {
     tags: ['role',],
     summary: 'search role by page',
     description: '',
     parameters: [{
       in: 'query',
       name: 'name',
       description: 'role\'s name',
     },
                  {
                    in: 'query',
                    name: 'pageIndex',
                    description: 'pageIndex',
                  },
                  {
                    in: 'query',
                    name: 'pageSize',
                    description: 'pageSize',
                  },
                 ],
     responses: {
       200: {
         description: 'SUCCEED',
         schema: {
           type: 'object',
           properties: {
             status: {
               type: 'string',
               description: 'status',
             },
             datas: {
               type: 'array',
               description: 'result datas',
               properties: {
                 token: {
                   type: 'string',
                   description: 'token',
                 },
               },
             },
             pageIndex: {
               type: 'number',
               description: 'pageIndex',
             },
             pageSize: {
               type: 'number',
               description: 'pageSize',
             },
             totalCount: {
               type: 'number',
               description: 'totalCount',
             },
           },
         },
       },
     },
   });
}
```

<a name="kLlul"></a>
#### 12.4.3 swagger的使用
> npm run dev   跑起来



![image.png](https://cdn.nlark.com/yuque/0/2019/png/271124/1556177097079-8b5f1bd3-0a96-4f8b-9501-4e8e26bff0a3.png#align=left&display=inline&height=57&name=image.png&originHeight=116&originWidth=1506&size=97669&status=done&width=746)

> 获取swgger地址 输入浏览器


> 你看到就是文档了


![image.png](https://cdn.nlark.com/yuque/0/2019/png/271124/1556177075826-0099e04f-9791-4449-ac74-1e4a035fde27.png#align=left&display=inline&height=337&name=image.png&originHeight=1300&originWidth=2878&size=161008&status=done&width=746)

> 点击try it out


![image.png](https://cdn.nlark.com/yuque/0/2019/png/271124/1556177147187-e83c3408-38ae-4507-945b-92ccfc8ac031.png#align=left&display=inline&height=253&name=image.png&originHeight=942&originWidth=2776&size=119431&status=done&width=746)

> 输入你传的值,然后点击Execute

![image.png](https://cdn.nlark.com/yuque/0/2019/png/271124/1556177241221-56d453ed-13e0-434d-a0ef-c547ddaf3a25.png#align=left&display=inline&height=251&name=image.png&originHeight=930&originWidth=2764&size=99436&status=done&width=746)

> 结果


![image.png](https://cdn.nlark.com/yuque/0/2019/png/271124/1556177347444-b29b2f31-3dc2-4a1d-9ec1-6e55cafd6544.png#align=left&display=inline&height=260&name=image.png&originHeight=1000&originWidth=2864&size=176157&status=done&width=746)

> 你就可以获取到接口传递过来的值,效果类似postman,但是清晰程度比postman好


<a name="p0Bhc"></a>
### 12.5 常见问题
一般情况下都不会有问题，但是如果你这时候巧妙的用了egg-static,那么你就会报错了<br />经过排查，你就会发现

> /node_modules/egg-swagger2/app.js


![image.png](https://cdn.nlark.com/yuque/0/2019/png/271124/1559286239507-15f599a8-e5fc-4252-8deb-77d4fa83ee90.png#align=left&display=inline&height=234&name=image.png&originHeight=468&originWidth=1190&size=124954&status=done&width=595)

它会是一个数组，然后报错必须是个字符串,然后你懂得..你给他做成一个字符串即可
