---
title: 5 css盒子模型
date: 2019-04-29 16:19:05
tags: css入门
desc: 
# keywords: 
categories:
  - css入门
# from: https://bitsofco.de/the-background-properties/
# demo: ../../../demos/201703/background.html
---
### 5.1 css盒子模型图解
![image.png](https://cdn.nlark.com/yuque/0/2019/png/271124/1555642917065-07173153-64c4-4418-aec3-260a0567d0af.png#align=left&display=inline&height=310&name=image.png&originHeight=310&originWidth=608&size=79782&status=done&width=608)

![image.png](https://cdn.nlark.com/yuque/0/2019/png/271124/1555643131585-10b0af93-c3d1-4bf2-8270-e82e69de0224.png#align=left&display=inline&height=326&name=image.png&originHeight=326&originWidth=388&size=34957&status=done&width=388)

- margin:外边距
- border:边框
- padding:内边距

<a name="bbfff0e4"></a>
### 5.2 css盒子模型之宽度和高度
1. px 像素写死<br />	2. % 动态计算的单位(自适应 响应式)<br /> 
```css
*{
	margin:0;
  padding:0;
}
.banner img{
	width:100%;
}
```

<a name="b421a9b5"></a>
### 5.3 内边距padding及简写

![image.png](https://cdn.nlark.com/yuque/0/2019/png/271124/1555644224943-24b67769-cf94-4589-99c0-db9ff5305a42.png#align=left&display=inline&height=304&name=image.png&originHeight=350&originWidth=858&size=143618&status=done&width=746)

<a name="60d1f72d"></a>
### 5.4 边框线border的使用技巧
> border:边框的宽度 边框线类型 边框线的颜色

<a name="3fcd0cf7"></a>
#### 5.4.1 边框线类型
<a name="81935414"></a>
#### 5.4.2 边框线类型

- solid 实线
- dashed 虚线
- dotted 点状线

<a name="cdb816d5"></a>
#### 5.4.3 边框线的颜色
|  | 黑色 | 白色 |
| --- | --- | --- |
| 颜色的英文 | black | white |
| # | #000 | #fff |
| rgb | rgb(0,0,0) | rgb(255,255,255) |

border:10px solid #000<br />如果没有知名方向的情况下，表示四个方向都相等<br />border-top  上边<br />border-right  右边<br />border-bottom 下边<br />border-left 左边

<a name="eb824421"></a>
#### 5.4.4 去掉边框
border:0<br />如果border属性只有边框段杜，没有边框的类型和颜色 导致border属性失效


<a name="bf7bbae0"></a>
#### 5.4.5 面试题(画个三角形)
![image.png](https://cdn.nlark.com/yuque/0/2019/png/271124/1555645454675-2f5867ec-b4f0-4928-b9aa-63abd50cf054.png#align=left&display=inline&height=144&name=image.png&originHeight=144&originWidth=494&size=26972&status=done&width=494)


```html
 /* 
    三角箭头原理：正方形的任意相邻的两条边线
    然后旋转一定的角度得到我们需要的任意方向的箭头 
    deg 角度单位 rotate旋转角度
    三角形的大小由正方形的宽高去控制
    三角形的粗细是有边框线去控制
    三角形的颜色是有边框线的颜色去控制
 */

<div class="arrow"></div>

<style>
.arrow{
  width: 0px;
  height: 0px;
  margin-top: 50px;
  margin-left: 50px;
  border-width:0 30px 30px;
  border-style:solid;
  border-color:transparent transparent #333;
  transform: rotate(90deg);//控制角度
}
</style>
```

<a name="edd6611e"></a>
### 5.5 padding
> 方向上和padding一致

<a name="3bdff0b3"></a>
### 5.6 margin的负值使用技巧
结构上不动，可以调换div顺序
<a name="f46b0c8a"></a>
### 5.7 padding和margin的区别
padding 是内边距<br />会影响我们在浏览器中看到的元素的实际大小内边距会让元素的内容增大和其它的元素没有关系<br />margin 是外边距<br />不会影响我们在浏览器中看到的元素的实际大小外边距不会让元素的内容增大和另一个元素的间距

![image.png](https://cdn.nlark.com/yuque/0/2019/png/271124/1555904206988-79943594-12d5-497a-a332-762df672d413.png#align=left&display=inline&height=292&name=image.png&originHeight=362&originWidth=924&size=146701&status=done&width=746)

<a name="95db6d8f"></a>
### 5.8 盒子模型的计算公式及使用技巧
> 元素实际宽度

宽度width + padding-left/padding-right+border-left/border-right
> 元素实际高度

高度height+padding-top/padding-bottom+border-top/border-bottom

口号: 元素的实际大小智慧padding和border的影响跟margin没有半毛钱的关系<br />如果加了padding和border的值要在width和height的值上减去padding和border的值 否则内容会溢出


