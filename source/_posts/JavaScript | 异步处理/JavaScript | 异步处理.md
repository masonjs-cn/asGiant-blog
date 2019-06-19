---
title: 异步处理
date: 2019-05-13 22:21:18
tags: 异步处理
desc: 所谓"异步"，简单说就是一个任务分成两段，先执行第一段，然后转而执行其他任务，等做好了准备，再回过头执行第二段,比如，有一个任务是读取文件进行处理，异步的执行过程就是下面这样。
# keywords: 
categories:
  - 异步处理
# from: https://bitsofco.de/the-background-properties/
# demo: ../../../demos/201703/background.html
---

## 异步
- 所谓"异步"，简单说就是一个任务分成两段，先执行第一段，然后转而执行其他任务，等做好了准备，再回过头执行第二段,比如，有一个任务是读取文件进行处理，异步的执行过程就是下面这样。


![image.png](https://cdn.nlark.com/yuque/0/2019/png/271124/1557757262806-925ce8b5-4d7c-4cfd-bbad-bf55f6a1650e.png#align=left&display=inline&height=377&name=image.png&originHeight=754&originWidth=2010&size=464212&status=done&width=1005)

这种不连续的执行，就叫做异步。相应地，连续的执行，就叫做同步。

## 高阶函数
> 函数作为一等公民,可以作为参数和返回值,也可以作为函数的参数


### 可以用于批量生成函数
```javascript
// 判断一个参数是否是字符串
function isString(param){
	return Object.prototype.toString.call(param) == '[object String]';
}
isString(123);

// 判断一个参数是否是数组
function isArray(param){
	return Object.prototype.toString.call(param) == '[object Array]';
}
isArray([]);
```

> 函数可以作为返回值


```javascript
function isType(type){
	return function(param){
  	return Object.prototype.toString.call(param) == `[object ${type}]`;
  }
}
let isString = isType('String');
let isArray = isType('Array');
console.log(isString({}))
console.log(isArray([]))

```

### 可以用于需要调用多次才执行的函数
> 函数可以作为参数传到另外一个函数里面


```javascript
function eat(){
	console.log("吃完了")
}

// 让他执行几次才会执行
function after(times,fn){
  let count = 0;
	return function(){
  	if(count++==times){
       fn();
    }
  }
}

let newEat = after(3,eat);
newEat();
newEat();
newEat();
```

## 异步编程的语法目标，就是怎样让它更像同步编程,有以下几种

- 回调函数实现
- 事件监听
- 发布订阅
- Promise/A+ 和生成器函数
- async/await

## 回调
> 比如我现在要读取一个文件，异步读取


```javascript
let fs = require('fs');
fs.readFile('./1.txt','utf8',function(err,data){
	if(err){ // 如果err有值，就表示程序出错
  	console.log(err);
  }else{ // 如果err为空就表示成功没有错误
  	console.log(data);
  }
});
```

回调函数的问题

1. 无法捕捉错误 try catch return
1. 不能return
1. 回调地狱

```javascript
function read(filename){
	fs.readFile(filename,'utf8',function(err,data){
    if(err){ // 如果err有值，就表示程序出错
      console.log(err);
    }else{ // 如果err为空就表示成功没有错误
      console.log(data);
    }
  });
}

try{
	 read('1.txt');	
}catch(e){
	console.log(e);
}

console.log(2);
```

> 当你访问服务器的时候，比如请求一个html页面，比如用户列表。服务器一方面会去读取模板文件,可能是ejs、pug、jade、handlebar、另外一方面还要读取数据(可能会放在文件里，也可以会放在数据里)，它们都很慢，所以都是异步的.


- 这种写法很难看
- 非常难以维护
- 效率比较低,因为它是串行的 

```javascript
fs.readFile('./template.txt','utf8',function(err,template){
  fs.readFile('./data.txt','utf8',function(err,data){
    console.log(template+''+data);
  })
})
```

> 如何解决这个回调嵌套的问题

## 异步流程解决方案

### 通过事件发布订阅来实现
```javascript
// 这node核心模块中一个类，通过它可以穿件时间发射器的实例，里面有两个核心方法
// 一个叫on emit,on表示注册监听，emit表示发射事件
let EventEmitter = require('events');
let eve = new EventEmitter();
// 这个html对象是存放
let html = {}; // template data

// 监听数据获取成功事件,当事件发生之后调用回调函数
eve.on('ready',function(key,value){
	html[key] = value;
  if(Object.key(html).lenght==2){
  	console.log(html);
  }
})

fs.readFile('./template.txt','utf8',function(err,template){
  // 1事件名 2参数往后是传递给回调函数的参数
	eve.emit('ready','template',template);
})

fs.readFile('./data.txt','utf8',function(err,data){
  // 
	eve.emit('ready','data',data);
})
```

### 哨兵变量

```javascript
// 通过一个哨兵来解决
let html = {}
function done(key,value){
	html[key]=value;
  if(Object.keys(html).length===2){
  	console.log(html);
  }
};

fs.readFile('./template.txt','utf8',function(err,template){
	done("template",data)
})

fs.readFile('./data.txt','utf8',function(err,data){
	done("data",data)
})
```

```javascript
// 通过一个哨兵来解决
let html = {}

function render(lenght,cb){
	let html = {};
  if(Object.keys(html).length===lenght){
  	cb(html);
  }
}

let done = render(2,function(html){
	console.log(html);
});

fs.readFile('./template.txt','utf8',function(err,template){
	done("template",data)
})

fs.readFile('./data.txt','utf8',function(err,data){
	done("data",data)
})
```

### 生成器Generators/ yield
生成器是一个函数，可以用了生成迭代器<br />生成器函数和普通函数不一样，普通函数一旦调用一定会执行完<br />但是生成器函数中间可以展厅，可以执行一会歇一会

![image.png](https://cdn.nlark.com/yuque/0/2019/png/271124/1557331225522-7a607d4c-21c8-445b-b59b-5b81c7e26609.png#align=left&display=inline&height=152&name=image.png&originHeight=196&originWidth=594&size=66695&status=done&width=461)
> 生成器函数有一个特点，需要加个*
> 生成器有若干个阶段，如何划分这些阶段呢
> yield 定义通过迭代器协议从生成器函数返回的值。如果省略，则返回undefined。


```javascript
function *go(params) {
        console.log(1);
        // 此处的b是提供外界输入进来
        // 这一行实现输入和输出，本次的输出放在yield后面，下次的输入放在yield前面
        let b = yield 'a';
        console.log(2);
        let c = yield b;
        console.log(3);
        return c;
    }
// 生成器函数和普通函数的函数不一样，调用它的话，函数并不会立刻执行
// 它会返回生成器的迭代器，迭代器是一个对象，每调用一次next就可以返回一个值对象
let it = go();;
let r1 = it.next();
// 第一次调用next返回一个对象，此对象有两个属性，一个value就是yield后面那个值，一个是done表示是否迭代完成
console.log(r1); //{value:'a',done:false};
// next 第一次执行不需要传参，传参是没有意义的
let r2 = it.next('B值');//传给了b
console.log(r2); // {value:'a',done:false};
let r3 = it.next();// {value:undefined,done:true};
console.log(r3);
```

### Promise来处理
> Promise 对象是一个代理对象（代理一个值），被代理的值在Promise对象创建时可能是未知的。它允许你为异步操作的成功和失败分别绑定相应的处理方法（handlers）。 

### 例子
```javascript
let p1 = new Promise((resolve, reject) => {
     setTimeout(() => {
         resolve(1000)
     }, 1000);
});

p1.then(res=>{
	console.log(res)
})
```

#### promise.all
> 会接收到promise数组，如果promise全部完成了这个，promise才会成功，如果有一个失败，整体就失败了

同时异步请求多个数据的时候,会用all
```javascript
let p1 = new Promise((resolve, reject) => {
     setTimeout(() => {
         resolve(1000)
     }, 1000);
});

let p2 = new Promise((resolve, reject) => {
     setTimeout(() => {
         resolve(1000)
     }, 1000);
});

Promise.all([p1,p2]).then(res=>{
    console.log('====================================');
    console.log(res);
    console.log('====================================');
},err=>{
 		console.log('====================================');
    console.log(err);
    console.log('====================================');
})
```

> 原理


```javascript
function gen(times,cb) {
    let result = [],count=0
    return function(i,data){
        result[i] = data;
        if (++count == times) {
            cb(result);
        }
    }    
}

Promise.alls = function (promises) {
    return new Promise(function (resovle, reject) {
        let result = []
        let count =0
        let done = gen(promises.length,resovle)
        // function done(i,data){
        //     result[i] = data;
        //     if (++count== promises.length) {
        //         resovle(result)
        //     }
        // }
        for (let i = 0; i < promises.length; i++) {
        //   promises[i].then(done.bind(null,i));
             promises[i].then(function (data) {
                 done(i,data)
             }, reject);
        }
    })
}

Promise.alls([p1,p2]).then(res=>{
    console.log('====================================');
    console.log(res);
    console.log('====================================');
},error=>{
    console.log('====================================');
    console.log(error);
    console.log('====================================');
})
```

#### promise.race
> 会接收到一个promise数组，只要一个成功，则就成功了，只有一个失败就是失败了

当你有三个接口都不稳定，可你可以同时请求三个接口，谁先回来用谁的
```javascript
let p1 = new Promise((resolve, reject) => {
     setTimeout(() => {
         resolve(1000)
     }, 1000);
});

let p2 = new Promise((resolve, reject) => {
     setTimeout(() => {
         resolve(1000)
     }, 1000);
});

Promise.race([p1,p2]).then(res=>{
    console.log('====================================');
    console.log(res);
    console.log('====================================');
})
```

> 原理


```javascript
Promise.race = function (promises) {
    return new Promise(function (resovle, reject) {
        for (let i = 0; i < promises.length; i++) {
             promises[i].then(resovle, reject);
        }
    })
}
```

### Co
> co是一个为Node.js和浏览器打造的基于生成器的流程控制工具，借助于Promise，你可以使用更加优雅的方式编写非阻塞代码。
> 

```javascript
let fs = require('fs');
function readFile(filename) {
  return new Promise(function (resolve, reject) {
    fs.readFile(filename, function (err, data) {
      if (err)
        reject(err);
      else
        resolve(data);
    })
  })
}
function *read() {
  let template = yield readFile('./template.txt');
  let data = yield readFile('./data.txt');
  return template + '+' + data;
}
co(read).then(function (data) {
  console.log(data);
}, function (err) {
  console.log(err);
});
```

```javascript
function co(gen) {
  let it = gen();
  return new Promise(function (resolve, reject) {
    !function next(lastVal) {
      let {value, done} = it.next(lastVal);
      if (done) {
        resolve(value);
      } else {
        value.then(next, reason => reject(reason));
      }
    }();
  });
}
```

### Async/ await
> 使用`async`关键字，你可以轻松地达成之前使用生成器和co函数所做到的工作
> 但是其实是它，只要generator+promise语法


> Async的优点

- 内置执行器
- 更好的语义
- 更广的适用性

```javascript
async function timeout() {
   return 'hello world'
}

timeout().then(res=>{
  console.log(res);
})
console.log('虽然在后面，但是我先执行');
```

async 返回是一个 promise

![image.png](https://cdn.nlark.com/yuque/0/2019/png/271124/1557754213539-5dd81bf9-7cea-4542-953a-1cd7a17b77fc.png#align=left&display=inline&height=60&name=image.png&originHeight=120&originWidth=666&size=22068&status=done&width=333)

> 举一个例子
> 

```javascript
function loading(num) {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve(2 * num)
        }, 2000);
    } )
}
// 这是一个函数构造器
```

> 这时候我想传入三个值30、50、40 通过计算后求和。
> 延迟的时间模拟网络请求时间


```javascript
async function testResult() {
  let one = await loading(30);
  let two = await loading(50);
  let three = await loading(40);
  console.log(first + second + third);
}

testResult();
```