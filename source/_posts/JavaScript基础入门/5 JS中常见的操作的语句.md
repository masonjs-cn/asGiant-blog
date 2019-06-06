---
title: 5.JS中常见的操作的语句
date: 2019-04-09 16:10:04
tags: JavaScript基础入门
desc: 
# keywords: 
categories:
  - JavaScript基础入门
# from: https://bitsofco.de/the-background-properties/
# demo: ../../../demos/201703/background.html
---

## if、else if 、else
> 判断操作语句


```javascript
if(条件1){
	//=>条件1成立执行的操作
}else if(条件2){
	//=>上面条件不成立，条件2成立，执行的操作
}
...
else{
	// => 以上条件都不成立执行的操作
}
```

如果好几个条件都成立了，只吧第一个成立的条件执行，后面成立的条件忽略不管<br />条件:

```javascript
A==B、A!=B、A>B、A<B

if(A){} // 先把A转换为布尔类型，判断真假以此来决定是否成立

//否成立

if(A>B&&A<10){} //只有两个小条件都是真，整体条件为真

if(A>B||A<10){}  // 只要其中一个小条件成立，整体条件是真
```

> BAT 面试题


```javascript
var num = parseFloat('width:12.5px');
if(num==12.5){ // =>NaN
	alert(12.5);
}else if(num==NaN){ // NaN!=NaN
	alert(NaN);
}else if(typeof num=='number'){ // 
	alert(0)
}else{
	alert("啥也不是")
}
```

## 三元运算符
> 条件？条件成立执行：条件不成立执行

if(条件){}else : 三元运算符就是这种简单if..else..的另一种写法

```javascript
var num = 10;
if(num>5&&num<10){
	num++;//累加1
}else{
	num--;
}
// 修改成为三元运算符,如果条件成立或者不成立的某一种情况并不需要什么处理
// 我们空着语法不符合，我们使用null、undefined、void 0(就是undefined)占位就可以
num>5&&num<10?num++:num--;
```

```javascript
var num = 10;
if(num>5 && num<10){
	num++;
  break;/continue;/return;
}
// => 修改成为三元运算符
// 在三元运算符的操作中不能出现break、continue、return这样的关键词，所以我们无法用三目代替if、else
num>5 && num<10?
(num++,return):null;
```

## swith case
> swith case应用于if、else中一个变量在不同值情况下的不同操作
> 

```javascript
var num =10;
switch(num){
	//switch后面小括号中存放的是一个值(一般我们都写变量;把变量存储的值拿来用，有时候也可能是一个计算)
  case 1:
    // case后面放的都是值，目的验证switch后面的值和哪一种case后面的值相等，相等的进行对应的处理
  	...
    break;
    // 每一种case借宿后都要加break借宿当前的判断
  case 10:
  	...
    break;
  default:
    // switch后面的值和每一种case情况对应的值都不相等，执行最后的default，类似于false
    ...
}
```

案例分析

```javascript
var num = 5;
switch(num%2){//=>先把取余操作进行运算，拿运算结果case比较
	case 0:
  num++;
  break;  //不加break，不管后面的条件是够成立，都会继续向下执行，知道遇到break为止
    			// 不加break，就可以实现||这样的操作
  case: 2-1: //case后面也应该是值，此处先把2-1计算，把计算的结果和switch值比较
  num--;
  // 最后一项可以不加break，不加也能跳出判断
  break;
}
num%2:让num存储的值除以2去余数(0或者1)
```

swich case 中的比较实用的"==="

- =:赋值，等号左边是变量，右边是值
- ==:比较，如果左边两边的类型不一样，浏览器默认转换为一样的然后再进行比较  '6'==6  => 6==6 =>true
- ===:绝对相等，不仅要求值一样，并且类型也要完全一样

## 循环操作语句
> 循环，重复做一件事情


```javascript
for(设置循环起始值；设置循环执行的条件；步长累加){
	// 循环体:重复做的事情都是在循环体重
}
```

- 设置初始值
- 验证条件
- 条件成立，执行循环体:不成立，循环借宿
- 步长累加

```javascript
for(;i<5;;){
	consloe.log(i);
  //没有步长累加，我们的i永远是0，循环条件永远成立“死循环”;
  //项目中不能出现死循环，一旦出现,循环下面的事情都做不了
}
```

### continue
> 结束本轮循环，继续执行下一轮:循环体重continue后面的代码都不会在执行，它会直接的去执行步长，然后进行下一轮


```javascript
for(var i=0;i<5;i+=2){
	console.log(i)
  continue;
}
```

### break
> 结束整个循环:循环体重一旦遇到break首先后面代码不执行了，而且步长累加也不执行了，循环都结束了


```
for(var i=0;i<5;i+=2){
	console.log(i)
  break;
}
```

> BAT面试题

```javascript
for(var i=1;i<10;i+=2){
	if(i<5){
  	i++;
    continue;
  }else{
  	i+=3;
    break;
  }
  console.log(i)
}
console.log(i) // =>10
```

### for in
> 用来遍历(循环)对象键值对的

- var key;var attr(attribute);
- 对象中有多少键值对，我们的for in 循环遍历多少次(多少次)
- 第一次循环key这个遍历存储的都是当前循环这个组键值队的属性名
- key存储的值都是字符串格式的(不管属性名是否为数字)
- 在for in 循环的遍历时候，大部分浏览器都是先把对象中的键值对进行排序(把数字属性的排在前面，并且排列的时候安卓数字由小达大排列),其次在把非数字的属性名按照之前编写的顺序，循环的时候按照重新排列循序一次遍历(小数算作字母不要做数字)

```javascript
var obj = {name:wjw,age:8,0:'wjh',3:'ylp',1:'cx'}
for(var key in obj){
    console.log('ok')
    // key 属性名 string
    console.log(obj.key)
  	//获取obj中key这个属性对应的值 ->undefined <=> obj['key']
    console.log(obj[key]);
  	//->每一次循环把key变脸存储的值(当前遍历的属性名)获取到放在中括号中，获取obj对应的属性值
}
for(var key in obj){
    if(obj.hasOwnProperty(key)){
        
    }
 
}
```

