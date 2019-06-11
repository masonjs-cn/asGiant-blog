---
title: 1 axios中文文档
date: 2019-06-11 19:19:05
tags: axios
desc: 
# keywords: 
categories:
  - axios
# from: https://bitsofco.de/the-background-properties/
# demo: ../../../demos/201703/background.html
---

<a name="oKOZX"></a>
## [](http://www.axios-js.com/zh-cn/docs/#%E4%BB%80%E4%B9%88%E6%98%AF-axios%EF%BC%9F)什么是 axios？
Axios 是一个基于 promise 的 HTTP 库，可以用在浏览器和 node.js 中。
<a name="axios"></a>
# [](http://www.axios-js.com/zh-cn/docs/#axios)axios
[![](https://img.shields.io/npm/v/axios.svg?style=flat-square#align=left&display=inline&height=20&originHeight=20&originWidth=88&status=done&width=88)](https://www.npmjs.org/package/axios)<br />[![](https://img.shields.io/travis/axios/axios.svg?style=flat-square#align=left&display=inline&height=20&originHeight=20&originWidth=88&status=done&width=88)](https://travis-ci.org/axios/axios)<br />[![](https://img.shields.io/coveralls/mzabriskie/axios.svg?style=flat-square#align=left&display=inline&height=20&originHeight=20&originWidth=96&status=done&width=96)](https://coveralls.io/r/mzabriskie/axios)<br />[![](https://img.shields.io/npm/dm/axios.svg?style=flat-square#align=left&display=inline&height=20&originHeight=20&originWidth=142&status=done&width=142)](http://npm-stat.com/charts.html?package=axios)<br />[![](https://img.shields.io/gitter/room/mzabriskie/axios.svg?style=flat-square#align=left&display=inline&height=20&originHeight=20&originWidth=90&status=done&width=90)](https://gitter.im/mzabriskie/axios)<br />[![](https://cdn.nlark.com/yuque/0/2019/svg/271124/1560250004028-3c53945d-a580-4506-bd3a-a4f7b19494d5.svg#align=left&display=inline&height=20&originHeight=20&originWidth=109&size=0&status=done&width=109)](https://www.codetriage.com/axios/axios)<br />Axios 是一个基于 promise 的 HTTP 库，可以用在浏览器和 node.js 中。
<a name="6Pi76"></a>
## [](http://www.axios-js.com/zh-cn/docs/#%E7%89%B9%E6%80%A7)特性

- 从浏览器中创建 [XMLHttpRequests](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest)
- 从 node.js 创建 [http](http://nodejs.org/api/http.html) 请求
- 支持 [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) API
- 拦截请求和响应
- 转换请求数据和响应数据
- 取消请求
- 自动转换 JSON 数据
- 客户端支持防御 [XSRF](http://en.wikipedia.org/wiki/Cross-site_request_forgery)

<a name="FL5o3"></a>
## [](http://www.axios-js.com/zh-cn/docs/#%E6%B5%8F%E8%A7%88%E5%99%A8%E6%94%AF%E6%8C%81)浏览器支持
|  | ![](https://cdn.nlark.com/yuque/0/2019/png/271124/1560250004759-3575626d-d083-496e-b471-758f9ec664e7.png#align=left&display=inline&percent=0&size=0&status=done) | ![](https://cdn.nlark.com/yuque/0/2019/png/271124/1560250006923-c67547d7-a258-4726-ab88-7b129d3fdf57.png#align=left&display=inline&percent=0&size=0&status=done) | ![](https://cdn.nlark.com/yuque/0/2019/png/271124/1560250004234-440efe9c-c7b2-4546-a0ed-9664320de551.png#align=left&display=inline&percent=0&size=0&status=done) | ![](https://cdn.nlark.com/yuque/0/2019/png/271124/1560250005544-9d6b7dca-e7ec-45d9-8eb1-df8d51d17550.png#align=left&display=inline&percent=0&size=0&status=done) | ![](https://cdn.nlark.com/yuque/0/2019/png/271124/1560250004449-6fcd8996-f3d8-43d2-9576-6c4971a2a43d.png#align=left&display=inline&percent=0&size=0&status=done) | ![](https://cdn.nlark.com/yuque/0/2019/png/271124/1560250005797-3133a7ce-e124-45fa-a646-e96ebd14b619.png#align=left&display=inline&percent=0&size=0&status=done) |
| --- | :--- | :--- | :--- | :--- | :--- | :--- |
| Latest ✔ | Latest ✔ | Latest ✔ | Latest ✔ | Latest ✔ | 8+ ✔ |  |

[![](https://cdn.nlark.com/yuque/0/2019/svg/271124/1560250003320-5caf3430-01a7-4a77-8723-7e89d793b43d.svg#align=left&display=inline&height=140&originHeight=140&originWidth=560&size=0&status=done&width=560)](https://saucelabs.com/u/axios)
<a name="0LEKx"></a>
## [](http://www.axios-js.com/zh-cn/docs/#%E5%AE%89%E8%A3%85)安装
使用 npm:<br />使用 bower:

```bash
npm install axios
```

```bash
bower install axios
```

使用 cdn:

| <script src="https://unpkg.com/axios/dist/axios.min.js"></script> |
| :--- |

<a name="dHRd3"></a>
## [](http://www.axios-js.com/zh-cn/docs/#%E6%A1%88%E4%BE%8B)案例

执行 `GET` 请求

```javascript
// 为给定 ID 的 user 创建请求
axios.get('/user?ID=12345')
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });

// 上面的请求也可以这样做
axios.get('/user', {
    params: {
      ID: 12345
    }
})
.then(function (response) {
    console.log(response);
})
.catch(function (error) {
    console.log(error);  
});
```


执行 `POST` 请求

```javascript
axios.post('/user', {
    firstName: 'Fred',
    lastName: 'Flintstone'
  })
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });
```

执行多个并发请求

```javascript
function getUserAccount() {
  return axios.get('/user/12345');
}

function getUserPermissions() {
  return axios.get('/user/12345/permissions');
}

axios.all([getUserAccount(), getUserPermissions()])
  .then(axios.spread(function (acct, perms) {
    // 两个请求现在都执行完成
}));
```

<a name="axios-API"></a>
## axios API
可以通过向 `axios` 传递相关配置来创建请求
<a name="axios-config"></a>
##### [](http://www.axios-js.com/zh-cn/docs/#axios-config)axios(config)

```javascript
// 发送 POST 请求
axios({
  method: 'post',
  url: '/user/12345',
  data: {
    firstName: 'Fred',
    lastName: 'Flintstone'
  }
});
```

```javascript
// 获取远端图片
axios({
  method:'get',
  url:'http://bit.ly/2mTM3nY',
  responseType:'stream'
})
  .then(function(response) {
  response.data.pipe(fs.createWriteStream('ada_lovelace.jpg'))
});
```

<a name="axios-url-config"></a>
##### [](http://www.axios-js.com/zh-cn/docs/#axios-url-config)axios(url[, config])

```javascript
// 发送 GET 请求（默认的方法）
axios('/user/12345');
```

<a name="IDEjU"></a>
### [](http://www.axios-js.com/zh-cn/docs/#%E8%AF%B7%E6%B1%82%E6%96%B9%E6%B3%95%E7%9A%84%E5%88%AB%E5%90%8D)请求方法的别名
为方便起见，为所有支持的请求方法提供了别名
<a name="axios-request-config"></a>
##### [](http://www.axios-js.com/zh-cn/docs/#axios-request-config)axios.request(config)
<a name="axios-get-url-config"></a>
##### [](http://www.axios-js.com/zh-cn/docs/#axios-get-url-config)axios.get(url[, config])
<a name="axios-delete-url-config"></a>
##### [](http://www.axios-js.com/zh-cn/docs/#axios-delete-url-config)axios.delete(url[, config])
<a name="axios-head-url-config"></a>
##### [](http://www.axios-js.com/zh-cn/docs/#axios-head-url-config)axios.head(url[, config])
<a name="axios-options-url-config"></a>
##### [](http://www.axios-js.com/zh-cn/docs/#axios-options-url-config)axios.options(url[, config])
<a name="axios-post-url-data-config"></a>
##### [](http://www.axios-js.com/zh-cn/docs/#axios-post-url-data-config)axios.post(url[, data[, config]])
<a name="axios-put-url-data-config"></a>
##### [](http://www.axios-js.com/zh-cn/docs/#axios-put-url-data-config)axios.put(url[, data[, config]])
<a name="axios-patch-url-data-config"></a>
##### [](http://www.axios-js.com/zh-cn/docs/#axios-patch-url-data-config)axios.patch(url[, data[, config]])
<a name="ZPI4t"></a>
###### [](http://www.axios-js.com/zh-cn/docs/#%E6%B3%A8%E6%84%8F)注意
在使用别名方法时， `url`、`method`、`data` 这些属性都不必在配置中指定。
<a name="lWxvE"></a>
### [](http://www.axios-js.com/zh-cn/docs/#%E5%B9%B6%E5%8F%91)并发
处理并发请求的助手函数
<a name="axios-all-iterable"></a>
##### [](http://www.axios-js.com/zh-cn/docs/#axios-all-iterable)axios.all(iterable)
<a name="axios-spread-callback"></a>
##### [](http://www.axios-js.com/zh-cn/docs/#axios-spread-callback)axios.spread(callback)
<a name="5jmoU"></a>
### [](http://www.axios-js.com/zh-cn/docs/#%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B)创建实例
可以使用自定义配置新建一个 axios 实例
<a name="axios-create-config"></a>
##### [](http://www.axios-js.com/zh-cn/docs/#axios-create-config)axios.create([config])

```javascript
const instance = axios.create({
  baseURL: 'https://some-domain.com/api/',
  timeout: 1000,
  headers: {'X-Custom-Header': 'foobar'}
});
```

<a name="mxlZR"></a>
### [](http://www.axios-js.com/zh-cn/docs/#%E5%AE%9E%E4%BE%8B%E6%96%B9%E6%B3%95)实例方法
以下是可用的实例方法。指定的配置将与实例的配置合并。
<a name="axios-request-config-1"></a>
##### [](http://www.axios-js.com/zh-cn/docs/#axios-request-config-1)axios#request(config)
<a name="axios-get-url-config-1"></a>
##### [](http://www.axios-js.com/zh-cn/docs/#axios-get-url-config-1)axios#get(url[, config])
<a name="axios-delete-url-config-1"></a>
##### [](http://www.axios-js.com/zh-cn/docs/#axios-delete-url-config-1)axios#delete(url[, config])
<a name="axios-head-url-config-1"></a>
##### [](http://www.axios-js.com/zh-cn/docs/#axios-head-url-config-1)axios#head(url[, config])
<a name="axios-options-url-config-1"></a>
##### [](http://www.axios-js.com/zh-cn/docs/#axios-options-url-config-1)axios#options(url[, config])
<a name="axios-post-url-data-config-1"></a>
##### [](http://www.axios-js.com/zh-cn/docs/#axios-post-url-data-config-1)axios#post(url[, data[, config]])
<a name="axios-put-url-data-config-1"></a>
##### [](http://www.axios-js.com/zh-cn/docs/#axios-put-url-data-config-1)axios#put(url[, data[, config]])
<a name="axios-patch-url-data-config-1"></a>
##### [](http://www.axios-js.com/zh-cn/docs/#axios-patch-url-data-config-1)axios#patch(url[, data[, config]])
<a name="0QW5i"></a>
## [](http://www.axios-js.com/zh-cn/docs/#%E8%AF%B7%E6%B1%82%E9%85%8D%E7%BD%AE)请求配置
这些是创建请求时可以用的配置选项。只有 `url` 是必需的。如果没有指定 `method`，请求将默认使用 `get`方法。

```javascript
{
   // `url` 是用于请求的服务器 URL
  url: '/user',

  // `method` 是创建请求时使用的方法
  method: 'get', // default

  // `baseURL` 将自动加在 `url` 前面，除非 `url` 是一个绝对 URL。
  //  它可以通过设置一个 `baseURL` 便于为 axios 实例的方法传递相对 URL
  baseURL: 'https://some-domain.com/api/',

  // `transformRequest` 允许在向服务器发送前，修改请求数据
  // 只能用在 'PUT', 'POST' 和 'PATCH' 这几个请求方法
  // 后面数组中的函数必须返回一个字符串，或 ArrayBuffer，或 Stream
  transformRequest: [function (data, headers) {
    // 对 data 进行任意转换处理
    return data;
  }],

  // `transformResponse` 在传递给 then/catch 前，允许修改响应数据
  transformResponse: [function (data) {
    // 对 data 进行任意转换处理
    return data;
  }],

  // `headers` 是即将被发送的自定义请求头
  headers: {'X-Requested-With': 'XMLHttpRequest'},

  // `params` 是即将与请求一起发送的 URL 参数
  // 必须是一个无格式对象(plain object)或 URLSearchParams 对象
  params: {
    ID: 12345
  },

   // `paramsSerializer` 是一个负责 `params` 序列化的函数
  // (e.g. https://www.npmjs.com/package/qs, http://api.jquery.com/jquery.param/)
  paramsSerializer: function(params) {
    return Qs.stringify(params, {arrayFormat: 'brackets'})
  },

  // `data` 是作为请求主体被发送的数据
  // 只适用于这些请求方法 'PUT', 'POST', 和 'PATCH'
  // 在没有设置 `transformRequest` 时，必须是以下类型之一：
  // - string, plain object, ArrayBuffer, ArrayBufferView, URLSearchParams
  // - 浏览器专属：FormData, File, Blob
  // - Node 专属： Stream
  data: {
    firstName: 'Fred'
  },

  // `timeout` 指定请求超时的毫秒数(0 表示无超时时间)
  // 如果请求话费了超过 `timeout` 的时间，请求将被中断
  timeout: 1000,

   // `withCredentials` 表示跨域请求时是否需要使用凭证
  withCredentials: false, // default

  // `adapter` 允许自定义处理请求，以使测试更轻松
  // 返回一个 promise 并应用一个有效的响应 (查阅 [response docs](#response-api)).
  adapter: function (config) {
    /* ... */
  },

 // `auth` 表示应该使用 HTTP 基础验证，并提供凭据
  // 这将设置一个 `Authorization` 头，覆写掉现有的任意使用 `headers` 设置的自定义 `Authorization`头
  auth: {
    username: 'janedoe',
    password: 's00pers3cret'
  },

   // `responseType` 表示服务器响应的数据类型，可以是 'arraybuffer', 'blob', 'document', 'json', 'text', 'stream'
  responseType: 'json', // default

  // `responseEncoding` indicates encoding to use for decoding responses
  // Note: Ignored for `responseType` of 'stream' or client-side requests
  responseEncoding: 'utf8', // default

   // `xsrfCookieName` 是用作 xsrf token 的值的cookie的名称
  xsrfCookieName: 'XSRF-TOKEN', // default

  // `xsrfHeaderName` is the name of the http header that carries the xsrf token value
  xsrfHeaderName: 'X-XSRF-TOKEN', // default

   // `onUploadProgress` 允许为上传处理进度事件
  onUploadProgress: function (progressEvent) {
    // Do whatever you want with the native progress event
  },

  // `onDownloadProgress` 允许为下载处理进度事件
  onDownloadProgress: function (progressEvent) {
    // 对原生进度事件的处理
  },

   // `maxContentLength` 定义允许的响应内容的最大尺寸
  maxContentLength: 2000,

  // `validateStatus` 定义对于给定的HTTP 响应状态码是 resolve 或 reject  promise 。如果 `validateStatus` 返回 `true` (或者设置为 `null` 或 `undefined`)，promise 将被 resolve; 否则，promise 将被 rejecte
  validateStatus: function (status) {
    return status >= 200 && status < 300; // default
  },

  // `maxRedirects` 定义在 node.js 中 follow 的最大重定向数目
  // 如果设置为0，将不会 follow 任何重定向
  maxRedirects: 5, // default

  // `socketPath` defines a UNIX Socket to be used in node.js.
  // e.g. '/var/run/docker.sock' to send requests to the docker daemon.
  // Only either `socketPath` or `proxy` can be specified.
  // If both are specified, `socketPath` is used.
  socketPath: null, // default

  // `httpAgent` 和 `httpsAgent` 分别在 node.js 中用于定义在执行 http 和 https 时使用的自定义代理。允许像这样配置选项：
  // `keepAlive` 默认没有启用
  httpAgent: new http.Agent({ keepAlive: true }),
  httpsAgent: new https.Agent({ keepAlive: true }),

  // 'proxy' 定义代理服务器的主机名称和端口
  // `auth` 表示 HTTP 基础验证应当用于连接代理，并提供凭据
  // 这将会设置一个 `Proxy-Authorization` 头，覆写掉已有的通过使用 `header` 设置的自定义 `Proxy-Authorization` 头。
  proxy: {
    host: '127.0.0.1',
    port: 9000,
    auth: {
      username: 'mikeymike',
      password: 'rapunz3l'
    }
  },

  // `cancelToken` 指定用于取消请求的 cancel token
  // （查看后面的 Cancellation 这节了解更多）
    
  cancelToken: new CancelToken(function (cancel) {
  })
}
```

<a name="RChKT"></a>
## [](http://www.axios-js.com/zh-cn/docs/#%E5%93%8D%E5%BA%94%E7%BB%93%E6%9E%84)响应结构
某个请求的响应包含以下信息

```javascript
{
  // `data` 由服务器提供的响应
  data: {},

  // `status` 来自服务器响应的 HTTP 状态码
  status: 200,

  // `statusText` 来自服务器响应的 HTTP 状态信息
  statusText: 'OK',

  // `headers` 服务器响应的头
  headers: {},

   // `config` 是为请求提供的配置信息
  config: {},
 // 'request'
  // `request` is the request that generated this response
// It is the last ClientRequest instance in node.js (in redirects)
  // and an XMLHttpRequest instance the browser
  request: {}
}
```

使用 `then` 时，你将接收下面这样的响应 :

```javascript
axios.get('/user/12345')
  .then(function(response) {
    console.log(response.data);
    console.log(response.status);
    console.log(response.statusText);
    console.log(response.headers);
    console.log(response.config);
});
```

在使用 `catch` 时，或传递 [rejection callback](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/then) 作为 `then` 的第二个参数时，响应可以通过 `error` 对象可被使用，正如在[错误处理](https://www.kancloud.cn/yunye/axios/234845#handling-errors)这一节所讲。
<a name="Mu5lc"></a>
## [](http://www.axios-js.com/zh-cn/docs/#%E9%85%8D%E7%BD%AE%E9%BB%98%E8%AE%A4%E5%80%BC)配置默认值
你可以指定将被用在各个请求的配置默认值
<a name="4X00K"></a>
### [](http://www.axios-js.com/zh-cn/docs/#%E5%85%A8%E5%B1%80%E7%9A%84-axios-%E9%BB%98%E8%AE%A4%E5%80%BC)全局的 axios 默认值

```javascript
axios.defaults.baseURL = 'https://api.example.com';
axios.defaults.headers.common['Authorization'] = AUTH_TOKEN;
axios.defaults.headers.post['Content-Type'] = 'application/x-www-form-urlencoded';
```

<a name="fL3j3"></a>
### 自定义实例默认值

```javascript
// Set config defaults when creating the instance
const instance = axios.create({
  baseURL: 'https://api.example.com'
});

// Alter defaults after instance has been created
instance.defaults.headers.common['Authorization'] = AUTH_TOKEN;
```

<a name="54SPH"></a>
### [](http://www.axios-js.com/zh-cn/docs/#%E9%85%8D%E7%BD%AE%E7%9A%84%E4%BC%98%E5%85%88%E9%A1%BA%E5%BA%8F)配置的优先顺序
配置会以一个优先顺序进行合并。这个顺序是：在 `lib/defaults.js` 找到的库的默认值，然后是实例的 `defaults` 属性，最后是请求的 `config` 参数。后者将优先于前者。这里是一个例子：

```javascript
// 使用由库提供的配置的默认值来创建实例
// 此时超时配置的默认值是 `0`
var instance = axios.create();

// 覆写库的超时默认值
// 现在，在超时前，所有请求都会等待 2.5 秒
instance.defaults.timeout = 2500;

// 为已知需要花费很长时间的请求覆写超时设置
instance.get('/longRequest', {
  timeout: 5000
});
```

<a name="3KiwC"></a>
## 拦截器
在请求或响应被 `then` 或 `catch` 处理前拦截它们。

```javascript
// 添加请求拦截器
axios.interceptors.request.use(function (config) {
    // 在发送请求之前做些什么
    return config;
  }, function (error) {
    // 对请求错误做些什么
    return Promise.reject(error);
  });

// 添加响应拦截器
axios.interceptors.response.use(function (response) {
    // 对响应数据做点什么
    return response;
  }, function (error) {
    // 对响应错误做点什么
    return Promise.reject(error);
  });
```

如果你想在稍后移除拦截器，可以这样：

```javascript
const myInterceptor = axios.interceptors.request.use(function () {/*...*/});
axios.interceptors.request.eject(myInterceptor);
```

可以为自定义 axios 实例添加拦截器

```javascript
const instance = axios.create();
instance.interceptors.request.use(function () {/*...*/});
```

<a name="NU04k"></a>
## 错误处理

```javascript
axios.get('/user/12345')
  .catch(function (error) {
    if (error.response) {
      // The request was made and the server responded with a status code
      // that falls out of the range of 2xx
      console.log(error.response.data);
      console.log(error.response.status);
      console.log(error.response.headers);
    } else if (error.request) {
      // The request was made but no response was received
      // `error.request` is an instance of XMLHttpRequest in the browser and an instance of
      // http.ClientRequest in node.js
      console.log(error.request);
    } else {
      // Something happened in setting up the request that triggered an Error
      console.log('Error', error.message);
    }
    console.log(error.config);
  });
```

Y可以使用 `validateStatus` 配置选项定义一个自定义 HTTP 状态码的错误范围。

```javascript
axios.get('/user/12345', {
  validateStatus: function (status) {
    return status < 500; // Reject only if the status code is greater than or equal to 500
  }
})
```

<a name="WjSiN"></a>
## 取消
使用 _cancel token_ 取消请求
> Axios 的 cancel token API 基于[cancelable promises proposal](https://github.com/tc39/proposal-cancelable-promises)，它还处于第一阶段。

可以使用 `CancelToken.source` 工厂方法创建 cancel token，像这样：

```javascript
const CancelToken = axios.CancelToken;
const source = CancelToken.source();

axios.get('/user/12345', {
  cancelToken: source.token
}).catch(function(thrown) {
  if (axios.isCancel(thrown)) {
    console.log('Request canceled', thrown.message);
  } else {
     // 处理错误
  }
});

axios.post('/user/12345', {
  name: 'new name'
}, {
  cancelToken: source.token
})

// 取消请求（message 参数是可选的）
source.cancel('Operation canceled by the user.');
```

还可以通过传递一个 executor 函数到 `CancelToken` 的构造函数来创建 cancel token：

```javascript
const CancelToken = axios.CancelToken;
let cancel;

axios.get('/user/12345', {
  cancelToken: new CancelToken(function executor(c) {
    // executor 函数接收一个 cancel 函数作为参数
    cancel = c;
  })
});

// cancel the request
cancel();
```
> 
> 注意: 可以使用同一个 cancel token 取消多个请求

<a name="u3s3F"></a>
## [](http://www.axios-js.com/zh-cn/docs/#%E4%BD%BF%E7%94%A8-application-x-www-form-urlencoded-format)使用 application/x-www-form-urlencoded format
默认情况下，axios将JavaScript对象序列化为JSON。 要以application / x-www-form-urlencoded格式发送数据，您可以使用以下选项之一。
<a name="LwTtQ"></a>
### [](http://www.axios-js.com/zh-cn/docs/#%E6%B5%8F%E8%A7%88%E5%99%A8)浏览器
在浏览器中，您可以使用URLSearchParams API，如下所示：

```javascript
const params = new URLSearchParams();
params.append('param1', 'value1');
params.append('param2', 'value2');
axios.post('/foo', params);
```
> 
> 请注意，所有浏览器都不支持URLSearchParams（请参阅caniuse.com），但可以使用polyfill（确保填充全局环境）。

或者，您可以使用qs库编码数据：

```javascript
const qs = require('qs');
axios.post('/foo', qs.stringify({ 'bar': 123 }));
```

或者以另一种方式（ES6），

```javascript
import qs from 'qs';
const data = { 'bar': 123 };
const options = {
  method: 'POST',
  headers: { 'content-type': 'application/x-www-form-urlencoded' },
  data: qs.stringify(data),
  url,
};
axios(options);
```

<a name="Node-js"></a>
### Node.js
在node.js中，您可以使用querystring模块，如下所示：

```javascript
const querystring = require('querystring');
axios.post('http://something.com/', querystring.stringify({ foo: 'bar' }));
```

您也可以使用qs库。
<a name="Semver"></a>
## [](http://www.axios-js.com/zh-cn/docs/#Semver)Semver
在axios达到1.0版本之前，破坏性更改将以新的次要版本发布。 例如0.5.1和0.5.4将具有相同的API，但0.6.0将具有重大变化。
<a name="Promises"></a>
## [](http://www.axios-js.com/zh-cn/docs/#Promises)Promises
axios 依赖原生的 ES6 Promise 实现而[被支持](http://caniuse.com/promises). 如果你的环境不支持 ES6 Promise，你可以使用 [polyfill](https://github.com/jakearchibald/es6-promise).
<a name="TypeScript"></a>
## [](http://www.axios-js.com/zh-cn/docs/#TypeScript)TypeScript
axios包括TypeScript定义。

```javascript
import axios from 'axios';
axios.get('/user?ID=12345');
```

<a name="6eADL"></a>
## 资源

- [Changelog](https://github.com/axios/axios/blob/master/CHANGELOG.md)
- [Upgrade Guide](https://github.com/axios/axios/blob/master/UPGRADE_GUIDE.md)
- [Ecosystem](https://github.com/axios/axios/blob/master/ECOSYSTEM.md)
- [Contributing Guide](https://github.com/axios/axios/blob/master/CONTRIBUTING.md)
- [Code of Conduct](https://github.com/axios/axios/blob/master/CODE_OF_CONDUCT.md)
<a name="Credits"></a>
## [](http://www.axios-js.com/zh-cn/docs/#Credits)Credits
axios深受Angular提供的、\$http服务的启发。 最终，axios是为了在Angular之外使用而提供独立的类似\$http服的务。
<a name="6Fzhv"></a>
## [](http://www.axios-js.com/zh-cn/docs/#%E5%8D%8F%E8%AE%AE)协议
MIT
