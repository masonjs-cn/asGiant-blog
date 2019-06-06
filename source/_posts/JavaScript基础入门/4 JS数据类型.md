---
title: 4.JS数据类型
date: 2019-04-09 16:10:04
tags: JavaScript基础入门
desc: 
# keywords: 
categories:
  - JavaScript基础入门
# from: https://bitsofco.de/the-background-properties/
# demo: ../../../demos/201703/background.html
---

## 数据类型

### 基本数据类型（值类型）

- Number  数字
- String  字符串
  - 单引号包裹起来的都是字符串(单双号没有区别)
- Boolean  布尔
  - true false => 布尔值只有两个值
- null 空对象指针
- undefined  未定义

### 引用数据类型

- {}  普通对象
- []  数组
- /^$/ 正则
- ...

### function数据类型

- funciotn fn (){}

## 数据类型检查

-  typeof
  - 用来检测数据类型的运算符
-  instanceod
  - 检测某个实例是否属于这个类
-  constructor 
  - 获取当前实例的构造器
- Object prototype.toSting.call()
  - 获取当前实例的所属类信息


### typeof
操作符
typeof 是用来检测给定变量的数据类型的操作符。对一个值使用 typeof 操作符可能返回下列某个字符串：

```javascript
"undefined"
"boolean"
"string"
"number"
"object" // 如果这个值是对象或者null "function"
```

## 布尔值
> Boolean()

- 把其他数据类型的值转化为布尔类型
- 只有0、Nan、null、undefined这五个数据值转换为布尔类型的false，其余的都会变成true

![image.png](https://cdn.nlark.com/yuque/0/2019/png/271124/1552208177369-64842834-6cfb-404d-81bf-8aebbb3ccd6a.png#align=left&display=inline&height=305&name=image.png&originHeight=812&originWidth=412&size=151327&status=done&width=155)

> 叹号在JS中海油一个作用：取反，先把值转换为布尔类型，然后再去取反

![image.png](https://cdn.nlark.com/yuque/0/2019/png/271124/1552208350624-3136c9bb-8da6-4d5a-9f28-79a81a3a0b7d.png#align=left&display=inline&height=109&name=image.png&originHeight=218&originWidth=98&size=14063&status=done&width=49)

`!!`
> 在叹号取反的基础上取反，取反两次相当于没有操作，但是却已经其他类型值转化为布尔类型了，和Boolean是相同的效果  


## 字符串
> 在JS中单引号和双引号包起来的都是字符串


```javascript
12 - > number
'12' -> string
'[12,23]' -> string
```

### toString() 
第一种是使用几乎每个值都有的 toString()方法。多数情况下，调用 toString() 方法不必传递参数，但在调用数值的 toString()方法时，可以传递一个参数：输出数值的基数。默认情况下，toString() 方法以十进制格式返回数值的字符串表示。而通过传递基数，toString() 可以输出二进制、八进制、十六进制等。

```javascript
var num = 10;
alert(num.toString());    // "10"
alert(num.toString(2));  // "1010"
alert(num.toString(8));  // "12"
alert(num.toString(10));  // "10"
alert(num.toString(16));  // "A"
```

常用方法<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/271124/1552212096220-2e8a4a63-4ef0-4168-9a4a-466a64dfe772.png#align=left&display=inline&height=189&name=image.png&originHeight=276&originWidth=266&size=51778&status=done&width=182)

### number数字
> 0 12-22 12.5 js中多增加了一个number类型的数据NaN  typeof NaN -> Number


```javascript
var intNum = 55; // 十进制整数 var octalNum1 = 070; // 八进制的56
var octalNum1 = 079; // 无效的八进制数值——解析为79 
var octalNum1 = 08; // 无效的八进制数值——解析为8 
var hexNum1 = 0xA;  // 十六进制的10
var hexNum2 = 0x1F; // 十六进制的31
```

> 注意，八进制字面量在严格模式下是无效的，会导致抛出错误。

### 数值范围
ECMAScript 能够表示的最小数值保存在 Number.MIN_VALUE 中——在多数浏览器中，这个值是 5e-324；能够 Number.MAX_VALUE 中——在大多数浏览器中，这个值是1.7976931348623157e+308。如果某次计算的结果得到了一个超过JavaScript 数值范围的值，那么这个数值将会自动转换为 Infinity 值，如果这个数值是负数，则会转换成 -Infinity（负无穷），如果这个数值是正数，则会转换成Infinity（正无穷）。要确定一个数值是不是有穷的，可以使用 isFinite() 函数。

### NaN

- not a numer : 不是一个数，但是属于number类型
- NaN == NaN ： false , NaN 和任何其他值都不相等

### isNaN()

- 用来检测当前这个值是否是非有效数字，如果不是有效数字，检测的结果是true , 反之是有效数字则为false

```javascript
isNaN(0)   // ->false
isNaN(NaN) // ->true
```

- 当我们使用isNaN检测值的时候，检测的值不是number类型的，浏览器默认的吧值先转换为number类型，任何再去检测

```javascript
isNaN('12') //->false
```

### Number()

- 把其他数据类型值转化成number类型的值

```javascript
Number('12') // -> 12
Number('12px') // ->NaN
// 在使用Number转换的时候只要字符串中出现任何一个非有效数字字符，最后的结果都是NaN

Number(true) //-> 1 
Number(false) //-> 0
Number(null) // -> 0
Number(undefined) //->NaN


```

-  把引用数据类型转换成number，首先需要吧引用数据类型转为字符串（toString)，在把字符串转换为number即可

```javascript
Number([]) // -> ""
Number([12]) // -> 12
Number([12,13]) // -> 12,13 (,是非有效字符) -> NaN
Number({age:12}) // ->NaN
Number({}) // -> NaN
```

### pareInt

- 也是吧其他数据类型值转换为number，和Number方法在处理字符串的时候有所区别

```javascript
Number('12px') // -> NaN
parseInt('12px') // -> 12
```

- 提取规则：从左到右依次查找有效数字字符，知道遇到非有效数字字符为止（不管后端是否还有，都不找了）

```javascript
parseInt('12px13') // -> 12
```

### 数值转换
处理整数最常用的还是 parseInt() ，它会忽略字符前面的空格，直到找到第一个非空格字符。如果第一个字符不是数字字符或者负号，parseInt() 就会返回 NaN；也就是说，用 parseInt() 转换空字符串会返回 NaN 。如果第一个字符是数字字符， parseInt() 会继续解析第二个字符，直到解析完所有后续字符或者遇到了一个非数字字符。如果字符以“0x”开头且后面跟数字字符，会被解析为 16 进制整数；<br />以“0”开头且后面跟数字字符，会被解析为 8 进制整数。下面给出一些例子：

```javascript
var num1 = parseInt("1234blue");   // 1234
var num2 = parseInt("");     // NaN
var num3 = parseInt("0xA");    // 10(十六进制)
var num4 = parseInt(22.5);   // 22
var num5 = parseInt("70");     // 70
var num6 = parseInt("0xf");    // 15(十六进制)
```

### pareFloat

- 在pareInt的基础上可以识别小数点

```javascript
pareInt('12.5px') -> 12
pareFloat('12.5px') -> 12.5
```

## null 和undefined

- null : 空，没有
- undefined ：未定义，没有
- "" : 空字符串，没有
- 0: 也可以理解为没有

### 空字符串和null的区别

- 都是去去种树
- 空字符串属于去挖了个坑，但是没有种任何东西
- null属于连坑都没挖
- 空字符串相对于null来说开辟了内存地址，消耗了那么一丢丢的性能

### null和undefined的区别

- null一般都是暂时没有，预期中以后会有的(可能以后也没有达到预期)，在js中null都是手动先赋值为null，后期我们在给其赋具体值
- undefined:完全没有预料之内的

## Object 对象
> ECMAScript 中的对象其实就是一组数据和功能的集合。对象可以通过执行 new 操作符后跟要创建的对象类型的名称来创建。而创建 Object 类型的实例并为其添加属性和（或）方法，就可以创建自定义对象，如下所示：


```javascript
var o = new Object();
```

每一个对象都是由零到多组 属性名（key键）：属性值(value值) 组成的,或者说有多组键值对组成的，每一组键值对中间用逗号分隔

### 属性
> 描述这个对象特点特征的


```javascript
var obj ={name:'wjw',age:8};
```

### 获取
> 某个属性名对应的属性值或者数字格式的


```javascript
obj.name
obj['name']
```
### 存储
> 属性值可以是任何数据类型

- 对象名.属性名：忽略属性名的单双引号
- 对象名[属性名]：不能忽略单双引号

```javascript
// 如果属性名是数字如何操作
obj.0 语法不支持
obj[0] / obj['0'] 两种都支持
```

> 如果操作的属性名在对象中不存在，获取的结果是undefined
> 

```javascript
obj.sex // ->undefined
```

### 设置/修改
> 一个对象的属性名是不能重复的（唯一性），如果之前存在就是修改属性值的操作，反之不存在就是新的设置属性的操作


```javascript
obj.sex = '男';
obj['age'] = 9;
```

### 删除

#### 假删除:让其属性赋值为null，但是属性还是对象

```javascript
obj.sex = null;
```

#### 真删除:把整个属性都在对象中暴力移出

```javascript
delete obj.sex
```

### 基本数据类型 和 引用数据类型的区别
> JS是运行在浏览器中的(内核引擎)，浏览器会为JS提供赖以生存的环境（提供给js代码执行的环境）=> 全局作用域window(global)


```javascript
var a = 12;
var b = a; // 把A变量存储的值赋值给B
b = 13;
console.log(a);

var n ={name:'wjh'};
var m = n;
m.name = 'wjw'
console.log(n.name)
```

- 基本数据类型是按值操作的：基本数据类型的赋值的时候，是直接把值赋值给变量即可
- 引用数据类型是按照空间地址（引用地址）来操作的: var n = {name:'wjw'}
  - 先创建一个变量n
  - 浏览器首先会吧开辟一个新的存储控件（内存控件），目的是吧对象中需要存储的内容（键值对）分别的存储在这个空间中，为了方便后期找到这个空间，浏览器给空间设定一个地址（16进制）
  - 把空间的地址赋值给了变量

![image.png](https://cdn.nlark.com/yuque/0/2019/png/271124/1552297184317-5a20e4ac-2ac4-4b41-8388-31856879bd7d.png#align=left&display=inline&height=390&name=image.png&originHeight=780&originWidth=906&size=92890&status=done&width=453)

<a name="08ed45a7"></a>
### 4.9 function数据类型
> 函数数据类型也要按照引用地址来操作的

函数:具备一定功能的方法

```javascript
// => 创建函数:
function 函数名(){
	//=> 函数体:实现某一个功能的具体JS代码
}
// => 执行函数:相当于使用洗衣机洗衣服(如果函数只创建了，但是没有去执行，函数没有任何的意义)
// 函数名()
```

```javascript
function fn(){
	console.log(1+1);
}
fn; // => 输出函数本身
fn(); // => 把函数执行（吧函数体重实现功能的代码执行）
```

![image.png](https://cdn.nlark.com/yuque/0/2019/png/271124/1552306799475-e85f6b5c-ed1a-4793-8c0d-41d1d899d981.png#align=left&display=inline&height=221&name=image.png&originHeight=442&originWidth=876&size=270908&status=done&width=438)

形参：形式参数(变量)，函数的入口<br />当我们创建一个函数想要实现个功能的时候，发现有一些材料不清楚，只有当函数运行的时候，别人传递给我，我才知道，此时我们就需要设定入口,让用户执行的时候通过入口把值把我们

```javascript
function fn(num1,num2){
	console.log(num1+num2)
}
// 实参:函数执行传递给函数的具体值就是实参
fn(1,2);
fn(10,20);
```

### 数据类型转换
把其他数据类型转换为number类型<br />-> isNaN、Number、pareInt、parseFloat<br />-> 在进行数据加减乘除数学运算的时候

```javascript
// true -> 1 false->0
// ''->0  '12'->12  '12px'->NaN/12
// '小伙子'->NaN
// null -> 0 
// undefined-> NaN
{} /^$/ function() ->NaN
[]
[12]->'12'->12
['12,13']->'12,23'->NaN
// => 引用数据类型转换为数字
// 通过toString方法把数组转换为字符串，然后在调用Number转换为数字
```

### JS中的数据运算

- +、-、*、/加减乘除
- 除了加法有特殊性，其余的运算符都是数学运算，也是遇到非数字类型，需要把其转换为number再运算

```
1-'1' -> 0
10*null -> 0
10/undefined -> NaN
10*[10]->100
```
### 加法的特殊性:

- 在遇到字符串的时候，+不是数学运算，而是字符串拼接，只要不遇到字符串就是数学运算

```
1+'1' -> '11'
null+'1' -> ‘null1’

```

- 字符串拼接:是把其它的值转换为字符串然后再拼接(toString)
- 其它数据类型的toString是直接的把值用单(双)引号包起来极客，只有对象的特殊性，对象的有特殊性，对象.toStirng==='[Object Object]

### 将其它数据类型转换为布尔类型

- Boolean、！、！！
- 在条件判断的时候、也是转换为布尔类型，然后验证条件的真假
- 只有0、NaN、空字符串、null、undefined五个转换为false、其余的都是转换为true

```
[] -> true
-1 -> true

if(box){
		// => 首先把box变量存储的值获取到，转化为布尔类型，如果为true条件成立，反之不成立
}

if(3+'3px'){
	// 条件成立: 3 + '3px' = '33px' 
}
if(3-'3px'){
	// 条件不成立: 3-'3px' = NaN
}
```

### 在使用==进行比较的时候
> 在使用==进行比较的时候，如果左右两边的数据不相同，浏览器默认转换为相同的类型，然后在比较('==='不会这样操作)


```
// 对象和对象: 应用数据类型比较的空间地址不一样，不是一个空间
[] == [] -> false
var a ={}
var b = a;
a==b -> true
```

### 对象和数字:吧对象转换成数字

```
[]== 0 -> true
({})=== NaN -> false
NaN和自己不相等和其它任何值都不相等 
```

### 对象和字符串:把两边都转换为数字比较的

```
[]==='' -> true
```

### 对象和布尔值:把两边都转换成数字

```
[]==true ->  0==1 ->false
[]==false ->  0==0 ->true
![]==false ->  ![]  ->把数组变成为布尔在取反=false
false=false -> true
```

字符串和数字:字符串转换为数字<br />字符串和布尔:都转为数字<br />布尔和数字:布尔转换为数字

规律:两个等于号比较，左右两边数字值的类型不一样，浏览器会吧两边的类型都转换为数字然后再比较，但是null和undefined除外<br />null==undefined -> true<br />null===undefined -> false<br />null 和 undefined 和其它任何都不相等<br />null==0 -> false null以及undefined和其它任何值都不相等
