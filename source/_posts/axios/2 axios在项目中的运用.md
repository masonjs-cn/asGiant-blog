---
title: 2 axios在项目中的运用
date: 2019-06-11 20:19:05
tags: axios
desc: axios在项目中的运用
# keywords: 
categories:
  - axios
# from: https://bitsofco.de/the-background-properties/
# demo: ../../../demos/201703/background.html
---

```javascript
/**
 * 全站http配置
 *
 * axios参数说明
 * isSerialize是否开启form表单提交
 * isToken是否需要token
 */

import axios from 'axios'
import store from '@/store/';
import router from '@/router/router'
import { serialize } from '@/util/util'
import {getToken,getRoleTitle} from '@/util/auth' // 获取相对应的权限
import {Message} from 'element-ui' // 调用弹窗组件
import website from '@/config/website'; // statusWhiteList 通过此处，获取白名单，默认[400]
import NProgress from 'nprogress' // progress bar vue中的进度条
import 'nprogress/nprogress.css' // progress bar style
import Cookies from 'js-cookie'

axios.defaults.timeout = 20000; // 设置超时时间

// 返回其他状态吗
// 定义对于给定的HTTP 响应状态码是 resolve 或 reject  promise 。
// 如果 `validateStatus` 返回 `true` (或者设置为 `null` 或 `undefined`)，
// promise 将被 resolve; 否则，promise 将被 rejecte

axios.defaults.validateStatus = function (status) {
    return status >= 200 && status <= 500; // 默认的
};

//跨域请求，允许保存cookie
axios.defaults.withCredentials = true;

// NProgress Configuration
// 通过设置为false关闭加载旋转器。(默认值是ture)
NProgress.configure({
    showSpinner: false
});

//HTTPrequest拦截-添加请求拦截器
axios.interceptors.request.use(config => {
    
    NProgress.start() // start progress bar  加载器开始加载
    
    const meta = (config.meta || {}); // 
    
    const isToken = meta.isToken === false;
    
    if (getToken() && !isToken) {
        config.headers['Admin.Authority.Token.cashloan'] = getToken();
        // 'Bearer ' + getToken() // 让每个请求携带token--['Authorization']为自定义key 请根据实际情况自行修改
    }
    
    //headers中配置serialize为true开启序列化    是否开启form表单提交
    if (config.methods === 'post' && meta.isSerialize === true) {
        config.data =config.data => {
            let list = [];
            Object.keys(data).forEach(ele => {
                list.push(`${ele}=${data[ele]}`)
            })
            return list.join('&');
        };
    }
    
    return config
    
}, error => {
    return Promise.reject(error)
});

//HTTPresponse拦截-添加响应拦截器
axios.interceptors.response.use(res => {
    NProgress.done(); // 进度条关闭
    
    const status = Number(res.status) || 200; // 返回值必须是200
    
    const statusWhiteList = website.statusWhiteList || []; // 白名单 400
    
    const message = res.data.message || '未知错误'; // 确定的返回值或者是'未知错误'
   
    const code = res.data.code
    
    if (code === 11002) {
        Message({
            message,
            type: "error"
        })
    }

    if (code === 10004) {
        Message({
            message: "有另一台设备登录",
            type: 'error'
        })
        store.dispatch('FedLogOut').then(() => router.push({
            path: '/login'
        }));
    }
    
    if (code === 10001) {
        Message({
            message: "请重新登录",
            type: 'error'
        })
        Cookies.set('loading', true)
        store.dispatch('FedLogOut').then(() => router.push({
            path: '/login'
        }));
    }
    
    if (code === 10002) {
        Message({
            dangerouslyUseHTMLString: true,
            message: `接口为${res.request.custom.url}</br></br>${getRoleTitle()}没有权限`,
            type: 'error'
        })
    }

    if (code === 10003) {
        Message({
            dangerouslyUseHTMLString: true,
            message,
            type: 'error'
        })
    }

    if (code === 404) {
        Message({
            dangerouslyUseHTMLString: true,
            message: `接口为${res.request.custom.url}</br></br>${JSON.stringify(res.data)}`,
            type: 'error'
        })
     }

    if (code === 400) {
        
        if (res.data.message.includes('/')) {
            Message({
                dangerouslyUseHTMLString: true,
                message: message.split('/')[1],
                type: 'error'
            })
            return
        }

        Message({
            dangerouslyUseHTMLString: true,
            message: `${JSON.stringify(res.data)}`,
            type: 'error'
        })
         
    }

    if (code === 500) {
        if(!res.data.message.includes("TIMEOUT")){
            Message({
                dangerouslyUseHTMLString: true,
                message:`服务器故障，请稍后重试`,
                // message: `接口为${res.request.custom.url}</br></br>${JSON.stringify(res.data)}`,
                type: 'error'
            })
        }
     }

    //如果在白名单里则自行catch逻辑处理
    if (statusWhiteList.includes(status)) return Promise.reject(res);
    //如果是401则跳转到登录页面
    if (status === 401) store.dispatch('FedLogOut').then(() => router.push({ path: '/login' }));
    // 如果请求为非200否者默认统一处理
    if (status !== 200) {
        Message({
            message: message,
            type: 'error'
        })
        return Promise.reject(new Error(message))
    }
    return res;
}, error => {
    NProgress.done();
    return Promise.reject(new Error(error));
})

export default axios;
```

