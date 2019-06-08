---
title: 6 BFC机制
date: 2019-04-29 17:19:05
tags: css入门
desc: 
# keywords: 
categories:
  - css入门
# from: https://bitsofco.de/the-background-properties/
# demo: ../../../demos/201703/background.html
---

BFC全称是Block Formatting Context，即块格式化上下文。它是CSS2.1规范定义的，关于CSS渲染定位的一个概念。它是一个独立的渲染区域，只有Block-level box参与， 它规定了内部的Block-level Box如何布局，并且与这个区域外部毫不相干。
<a name="90097dcf"></a>
### 6.1 BFC布局规则

1. 内部的Box会在垂直方向，一个接一个地放置；
1. Box垂直方向的距离由margin决定。属于同一个BFC的两个相邻Box的margin会发生重叠；
1. 每个元素的margin box的左边， 与包含块border box的左边相接触(对于从左往右的格式化，否则相反)。即使存在浮动也是如此。；
1. BFC的区域不会与float box重叠，常用来清除浮动和布局。；
1. BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。反之也如此。；
1. 计算BFC的高度时，浮动元素也参与计算；
<a name="694ec134"></a>
### 6.2 会生成BFC的元素

- **根元素**或其它包含它的元素；
- **浮动** (元素的`float`不为`none`)；
- **绝对定位元素** (元素的`position`为`absolute`或`fixed`)；
- **行内块**`inline-blocks`(元素的 `display: inline-block`)；
- **表格单元格**(元素的`display: table-cell`，HTML表格单元格默认属性)；
- `overflow`的值不为`visible`的元素；
- **弹性盒 flex boxes** (元素的`display: flex`或`inline-flex`)；
<a name="50eaf095"></a>
### 6.3 BFC的范围
BFC的范围在MDN中是这样描述的。
> A block formatting context contains everything inside of the element creating it that is not also inside a descendant element that creates a new block formatting context.

中文的意思一个BFC包含创建该上下文元素的所有子元素，但不包括创建了新BFC的子元素的内部元素。<br />插入一段代码方便理解

```html
<div class='div_1 BFC'>
     <div class='div_2'>
         <div class='div_3'></div>
         <div class='div_4'></div>
      </div>
      <div class='div_5 BFC'>
	       <div class='div_6'></div>
         <div class='div_7'></div>
     </div>
</div>
```

`div_1`创建了一个块格式上下文，这个上下文包括了`div_2`、`div_3`、`div_4`、`div_5`。即`div_2`中的子元素也属于`div_1`所创建的BFC。但由于`div_5`创建了新的BFC，所以`div_6`和`div_7`就被排除在外层的BFC之外。<br />这就代表着**一个元素不能同时存在于多个BFC中。**<br />BFC的一个最重要的效果是，让处于BFC内部的元素与外部的元素相互隔离，使内外元素的定位不会相互影响。这是利用BFC清除浮动所利用的特性。
<a name="29b3a1c6"></a>
### 6.4 BFC的常用方式：
<a name="c0833039"></a>
#### 6.4.1 子级浮动导致父级高度塌陷

```html
<style type="text/css">
        .box{
            width: 900px;
            background: black;
          	height: 300px; // 增加高度
        }

        .box1{
            height: 300px;
            width: 300px;
            background: red;
            float: left;
        }

        .box2{
            height: 300px;
            width: 300px;
            background: blue;
            float: left;
        }

    </style>

......

<div class="box">
    <div class="box1"></div>
    <div class="box2"></div>
</div>
```

上面的代码定义了3个块，一个父级包含了两个子集，但是父级的背景颜色无法显示，是因为子集元素浮动导致了父级高度的塌陷。<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/271124/1555910652193-8245b415-d1ff-42f8-b7d8-cc23cd31ae61.png#align=left&display=inline&height=239&name=image.png&originHeight=476&originWidth=1486&size=17060&status=done&width=746)<br />
<br />在为box设置BFC后，box的高度才能找回来。<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/271124/1555910675579-27de4977-c9c8-4985-895f-935620f26047.png#align=left&display=inline&height=245&name=image.png&originHeight=484&originWidth=1476&size=14251&status=done&width=746)<br />从而显示出正确的样式。
<a name="d41d8cd9"></a>
#### 
<a name="d12cbf47"></a>
#### 6.4.2 子级margin-top将父级带下 为父级触发BFC
一个盒子有上边距 另一个有下边距 会出现margin边距的重叠问题<br />并列盒子的margin重写=>双margin的重叠<br />-> 取大值 并不是他们相加之和 也就是谁大听谁的
> 要将黑色块中的小红块下移一点，直接使用了margin-top，结果黑块一起下移了。


```html
<style type="text/css">
        .box{
            width: 300px;
            height: 300px;
            background: black;
        }

        .box1{
            height: 100px;
            width: 100px;
            background: red;
            margin-top: 50px;
        }

    </style>

......

<div class="box">
    <div class="box1"></div>
</div>
```
![](https://cdn.nlark.com/yuque/0/2019/png/271124/1555910696569-867333cb-63bd-4a4a-b7f5-7121b42e1331.png#align=left&display=inline&height=293&originHeight=664&originWidth=620&status=done&width=274)

而设置了BFC后，就能正确的下浮红色块

![](https://cdn.nlark.com/yuque/0/2019/png/271124/1555910705446-aaeb919d-7446-475f-aa13-b6fca56ac33d.png#align=left&display=inline&height=269&originHeight=598&originWidth=604&status=done&width=272)

> margin的兼容问题:margin top的传递问题

大盒子里面嵌套小盒子 给小盒子加margin-top 不但没有实现和大盒子之间的间距 反而传递给大盒子身上 导致整体下移动<br />解决兼容性问题

1. overflow:hidden  解决margin-top的传递问题(此处并没有溢出隐藏)
1. padding-方位:1px 这种方法影响最后实际宽高 需要在width/height上基础上减掉才不会影响最后实际的宽高
1. border-top:1px 这种方法会影响最后实际的高度 需要在高度height上基础上减掉 才不会影响最后实际的高度
1. 给子元素的margin-top的值改成父元素的padding-top,这样就避免使用margin-top值导致传递的问题
