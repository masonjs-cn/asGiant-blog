---
title: 4 CSS的三大特性 (继承属性)
date: 2019-04-29 15:19:05
tags: css入门
desc: 
# keywords: 
categories:
  - css入门
# from: https://bitsofco.de/the-background-properties/
# demo: ../../../demos/201703/background.html
---
### 4.2 无继承性的属性
<a name="3a314dd7"></a>
#### 4.2.1 display

- inline
- block
- inline-block
- table-cell
- none
> 规定元素应该生成的框的类型

<a name="ee565a76"></a>
#### 4.2.2 文本属性：
vertical-align：垂直文本对齐<br />text-decoration：规定添加到文本的装饰<br />text-shadow：文本阴影效果<br />white-space：空白符的处理<br />unicode-bidi：设置文本的方向
<a name="537665bf"></a>
#### 4.3.3 盒子模型的属性：
width、height、margin 、margin-top、margin-right、margin-bottom、margin-left、border、border-style、border-top-style、border-right-style、border-bottom-style、border-left-style、border-width、border-top-width、border-right-right、border-bottom-width、border-left-width、border-color、border-top-color、border-right-color、border-bottom-color、border-left-color、border-top、border-right、border-bottom、border-left、padding、padding-top、padding-right、padding-bottom、padding-left
<a name="245c3651"></a>
#### 4.3.4 背景属性
background、background-color、background-image、background-repeat、background-position、background-attachment
<a name="daef0428"></a>
#### 4.3.5 定位属性
float、clear、position、top、right、bottom、left、min-width、min-height、max-width、max-height、overflow、clip、z-index
<a name="d2c5cb06"></a>
#### 4.3.6 生成内容属性
content、counter-reset、counter-increment
<a name="d04fa3fe"></a>
#### 4.3.7 轮廓样式属性
outline-style、outline-width、outline-color、outline
<a name="cb8d84bf"></a>
#### 4.3.8 页面样式属性
size、page-break-before、page-break-after
<a name="1682a5fd"></a>
#### 4.3.9 声音样式属性
pause-before、pause-after、pause、cue-before、cue-after、cue、play-during

<a name="66582b23"></a>
### 4.3 有继承性的属性
<a name="16cb3fde"></a>
#### 4.3.1 字体系列属性
font：组合字体<br />font-family：规定元素的字体系列<br />font-weight：设置字体的粗细<br />font-size：设置字体的尺寸<br />font-style：定义字体的风格<br />font-variant：设置小型大写字母的字体显示文本，这意味着所有的小写字母均会被转换为大写，但是所有使用小型大写字体的字母与其余文本相比，其字体尺寸更小。<br />font-stretch：对当前的 font-family 进行伸缩变形。所有主流浏览器都不支持。<br />font-size-adjust：为某个元素规定一个 aspect 值，这样就可以保持首选字体的 x-height。
<a name="f2838a6b"></a>
#### 4.3.2 文本系列属性
text-indent：文本缩进<br />text-align：文本水平对齐<br />line-height：行高<br />word-spacing：增加或减少单词间的空白（即字间隔）<br />letter-spacing：增加或减少字符间的空白（字符间距）<br />text-transform：控制文本大小写<br />direction：规定文本的书写方向<br />color：文本颜色
<a name="00a2debd"></a>
#### 4.3.3 元素可见性
visibility
<a name="0cfcc79f"></a>
#### 4.3.4 表格布局属性
caption-side、border-collapse、border-spacing、empty-cells、table-layout
<a name="643dc764"></a>
#### 4.3.5 列表布局属性
list-style-type、list-style-image、list-style-position、list-style
<a name="d2c5cb06-1"></a>
#### 4.3.6 生成内容属性
quotes
<a name="a6a95512"></a>
#### 4.3.7 光标属性
cursor
<a name="42bb3516"></a>
#### 4.3.8 页面样式属性：
page、page-break-inside、windows、orphans
<a name="2c0d48c6"></a>
#### 4.3.9 声音样式属性：
speak、speak-punctuation、speak-numeral、speak-header、speech-rate、volume、voice-family、pitch、pitch-range、stress、richness、、azimuth、elevation

<a name="52035ff5"></a>
### 4.4 所有元素可以继承的属性
1、元素可见性：visibility<br />2、光标属性：cursor
<a name="c2c4d0fd"></a>
### 4.5 **内联元素可以继承的属性**
1、字体系列属性<br />2、除text-indent、text-align之外的文本系列属性
<a name="bd1843f1"></a>
### 4.6 **块级元素可以继承的属性**
1、text-indent、text-align
