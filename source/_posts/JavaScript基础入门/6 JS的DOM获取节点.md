---
title: 6.JS的DOM获取节点
date: 2019-04-09 17:10:04
tags: JavaScript基础入门
desc: 
# keywords: 
categories:
  - JavaScript基础入门
# from: https://bitsofco.de/the-background-properties/
# demo: ../../../demos/201703/background.html
---

> DOM:document object model 文档对象模型，提供一些属性和方法可以让我们去操作DOM元素

![image.png](https://cdn.nlark.com/yuque/0/2019/png/271124/1552464509901-7b6d49d4-6147-4355-9eed-3fa8568b4659.png#align=left&display=inline&height=150&name=image.png&originHeight=300&originWidth=450&size=41767&status=done&width=225)


![image.png](https://cdn.nlark.com/yuque/0/2019/png/271124/1552490736429-afc8138d-9713-4b29-9ec0-b80238f4d94f.png#align=left&display=inline&height=538&name=image.png&originHeight=1076&originWidth=1816&size=601570&status=done&width=908)



## 节点介绍
> node 节点，浏览器默认在一个html页面中的所有内容都是节点(包括标签、注解、文字文本等)

- 元素节点:HTML标签
- 文本节点:文字内容(大部分浏览器会把空格和换行也当做文本节点)
- 注解节点
- document文档节点

> 元素节点

- nodeType:1
  - 属性含有某个节点的名称
- nodeName: 大写标签名(在部分浏览器的怪异模式下，我们写的标签名是小写，它获取的就是小写...)
  - 对于元素节点，因为本身不直接包含文本，所以nodeValue是不可用的。当然你也可以在示例中自己写试试看有什么结果出现。
  - 对于文本节点，nodeValue=文本值
  - 对于属性节点，nodeValue=属性值 
- nodeValue:null
  - 对于元素节点，nodeType=1
  - 对于文本节点，nodeType=3
  - 对于属性节点，nodeType=2
  - 对于注释元素，nodeType=8
  - 对于文档元素，nodeType=9

[curEle].tagName:获取当前元素的标签名(获取的标签名一般都是大写)

> 文本节点

nodeType:3<br />nodeName:#text<br />nodeValue:文本内容

> 注释节点

nodeType:8<br />nodeName:#comment<br />nodeValue:注释内容

> 文档节点

nodeType:9<br />nodeName:#document<br />nodeValue:null

```html
<-- div#box>(ul>li{0$}*3)+div{内容$}*3-->
<div id="box">
        <ul>
            <li>01</li>
            <li>02</li>
            <li>03</li>
        </ul>
        <div>内容1</div>
        <div>内容2</div>
        <div>内容3</div>
 </div>
```


## 获取dom元素

### document.getElementById 一个元素

- 此方法的上下文只能document
- 一个html页面中元素的id理论上是不能重复的,如果页面中ID重复了，我们获得结果第一个id对应的元素对象
- 在ie7更低的版本浏览器中，会把表单元素的name值当做id来识别使用(项目中尽量不要让表单的name和其他元素的id相同)
- 如果我们把js放在结构的下面，我们可以直接使用id值获取这个元素(不需要通过getElementById获取)，而且这种方式会把页面中所有id是他的元素都获取到(元素对象，或者集合) => 不推荐

```javascript
<div id="box1"></div><div id="box2"></div><div id="box1"></div>
<script>
   console.log(box1)    // -> [div#box1, div#box1, box1: div#box1]
</script>
```


```html
<input id="myInput" type="text" size="20"/><br />
<script>
  var x=document.getElementsByName("myInput");
</script>
```

### document.getElementClassName 元素集合

- 上下文是可以自己来指定
- 获取到的结果是一个元素集合(类数组集合)

  

-  获取的结果是集合，哪怕集合中只有一项，我们想要操作的是这一项(元素对象)，需要先从集合中获取出来，然后再操作
- 但是真实的项目中我们经常会通过样式类名获取元素，getElementClassName这个方法在ie6-8不兼容的


```javascript
<input name="myInput" type="text" size="20"/><br />
<script>
  var x=document.getElementsByName("input");
</script>

var bodyBox = document.getElementsByTagName('body');
bodyBox[0].getElementsByTagName('div');
```


### document.getElementsTagName 元素集合

```html
<input name="myInput" type="text" size="20"/><br />
<script>
  var x=document.getElementsByName("input");
</script>
```

### document.getElementsByName 节点集合
> 通过元素的NAME属性值获取一组元素（类数组：节点集合NodeList）
> 他的上下文只能是document

- IE浏览器只能识别表单元素的name属性值，所以我们这个方法一般都用来操作表单元素的
- 获取html获得body的元素对象
```html
<input name="myInput" type="text" size="20"/><br />
<script>
 var x=document.getElementsByName("myInput");
</script>
```

### domcument.domcumentElement 获取整个html的对象

```javascript
 document.documentElement.clientWidth||document.body.clientWidth
 // 获取当前浏览器可视区域的宽度(当前页面一个屏幕的宽度)
 // =>clientHieght 获取高度

```

### domcument.body 获取body对象
### domcument.head 获取整个head对象
### [context]querySelector  一个元素对象 / [context]querySelectorAll 获取元素集合

- ie6-8不兼容，而且没有特别好的办法处理他的兼容，所以这两个方法一般多用于移动端开发使用

querySelector 获取一个元素对象<br />querySelectorAll 获取的一个元素集合<br />只要css支持的选择器，这里大部分都支持

```javascript
document.querySelector('#box1');
document.querySelectorAll('.box1');
document.querySelectorAll('div');
document.querySelectorAll('body>div');
document.querySelectorAll('#box1 li');
```

## 节点关系属性
> 节点是用来描述页面中每一部门之间关系的,只要我可以获取页面中的一个页面，那么我就可以通过相关的属性和方法获取页面中所有的节点


![image.png](https://cdn.nlark.com/yuque/0/2019/png/271124/1552635822022-57c9c5f8-f1bb-4e19-bd32-ce2c10156817.png#align=left&display=inline&height=175&name=image.png&originHeight=350&originWidth=764&size=48181&status=done&width=382)

### childNodes
> 获取当前元素所有的子节点(节点集合:类数组)
> 注:不仅仅是元素子节点，文本、注释等都会包含在内:子节点说明只是在儿子辈分中查找

### children
> 获取所有的元素子节点(元素集合)
> 在IE6-8下获取的结果和标准浏览器中有区别(IE6-8中会把注释点当做元素节点获取到)


### pareNode
> 获取当前元素的父节点(元素对象)


### previousibing 
> 获取当前节点的上一个各个节点上一个哥哥节点(不一定是元素节点也可能是文本或者注释)

### nextibling
> 获取当前节点的下一个弟弟节点

### previousElementbling
> 获取当前节点的上一个哥哥元素节点

### nextElementsIbling
> 获取当前节点下一个弟弟元素节点
> IE6-8不兼容

### firstChild
> 当前元素所有子节点中的第一个(也不一定是元素节点，可能是文本和注释)

### lastChild
> 当前元素多有子节点中的最后一个
> fistElementChild lastElementChild(IE6-8兼容)


## 创建和增加DOM元素
> 真实项目中，我们偶尔会在js中动态创建html标签，然后把其增加到页面中


### document.createElement
> 在js中动态创建一个html标签

### appendChild
> 容器.appendChild(新元素)
> 把当前创建的新元素添加到容器的末尾位置

### inserBefore
> 容器.inserBefore(新元素、老元素)
> 在当前容器中，把新创建的元素增加到老元素之前


```javascript
// 创建
var oDiv = document.createElement('div');
oDiv.id='div1';
oDiv.className = 'box';

// 添加到页面中
document.body.appendChild(oDiv);
document.body.inserBefore(oDiv,box2);
```

```javascript
var link = document.createElement('a');
link.href = 'http://www.baidu.com?name=1&age=2#haha'

consloe.dir(link);
// hash:存储饿哈希值 '#haha'
// hostname:域名 'www.baidu.com'
// pathname:路径 '/stu/'
// protocol:协议 'http:'
// search:问号传递参数值 '?nname=1&age=2'
```

真实项目中很多需要通过动态创建元素来完成的，其中有一个需求:解析一个url地址每一部分的信息(包括问号传值的参数值)

- 纯字符串拆分截取
- 编写强大的正则，捕获到需要的结果
- 通过动态创建一个a标签，利用a标签的一些内置属性来分别获取每一部分的内容

```javascript
function queryURLParameter(url){
	var link = document.createElement('a');
  link.href=url;
  
  var search = link.search,
  		obj = {}'
  if(search.length===0) return;
  search = search.substr(1).split(/&|=/g);
  for(var i=0;i<search.length;i+=2){
  	var key = search[i],
    		value = search[i+1];
    obj[key]=value;
  }
  link = null;
  return obj;
}
```

## 修改删除克隆DOM元素

### removeChild

- 容器.removeChild(元素)
- 在当前容器中把每一个元素移出掉

### replaceChild

- 容器.removeChild(新元素，老元素)
- 把原有的元素克隆一份一模一样的，false:只克隆当前元素本身，true:深度克隆，吧当前元素本身以及元素的所有后代都进行克隆
### [set/get/remove]Attribute

```javascript
给当前元素设置/获取/移出属性的(一般操作的都是它的自定义属性)
box.setAttribute('myIndex',0)
box.getAttribute('myIndex')
box.removeAttribute('myIndex')
```

> 使用xxx.index=0 和xxx.setAttribute('index',0)这两种设置自定义属性的区别

xxx.index : 是吧当前操作的元素当做一个普通对象，为其设置一个属性名<br />xxx.setAttribute:把元素当做特殊的元素对象来处理，设置的自定义属性是和页面结构中的DOM元素映射在一起的

JS中获取的元素对象，我们可以把他理解为两种角色:

- 与页面HTML结构无关的普通对象
- 与页面HTML结构存在映射关系的元素对象

元素对象中的内置属性，大部分都和页面的标签存在映射关系:<br />xxx.style.backgroundColor = 'xxx' 此时不仅把js中对象对应的属性值改变了，而且也会映射到页面的html标签上(标签中有一个style行内样式，元素的样式改变了)<br />xxx.className = 'xxx'此时不仅是吧js对象中的属性值改变了，而且页面中的标签增加了class样式类(可以看见的)

元素对象中的自定义属性: xxx.index=0<br />仅仅是吧js对象中增加了一个属性名(自定义的)，和页面中的html没啥关系(在结构上看不见)

xxx.setAttribute:通过这种方式设置的自定义属性和之前提到的内置属性差不多，都是和html结构存在映射关系的(设置的自定属性可以呈现在结构上)

## 6.6 面试题

> 把当前页面中所有id叫做box1的都获取到


```javascript
var allList = document.getElementsByTagName(*);
var result = []
for(var i=0;i<allList.length;i++){
	var item = allList[i];
  item.id === 'box1'?result.push(item)
}
console.log(result)
```

> 获取当前元素的上一个哥哥元素节点(兼容所有的浏览器)
> curEle:current element


```javascript
// 首先获取当前元素的上一个哥哥节点，判断当前获取的节点是否为元素节点(nodeType===1)
// 如果不是基于当前获取的节点，找他的上一个哥哥节点..(找几次不知道)一直到找到的节点是元素节点为止
// 如果在查找过程中，发现没有上一个哥哥节点，找到头了，则不再继续查找

function prev(curEle){
	var p = curEle.previousSibling; // 属性返回同一树层级中指定节点的前一个节点。
  while(p&&p.nodeType!==1){ //p:p!=null
    p = p.previousSibling;
  }
	return p;
}

// 扩展
// next: 获取下一个弟弟元素节点
// prevAll:获取所有的哥哥元素节点
// nextAll:获取所有的弟弟元素节点
// siblings:获取所有的兄弟元素节点
// index:获取当前元素的兄弟中排名索引
```

