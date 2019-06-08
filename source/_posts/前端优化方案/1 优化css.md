---
title: 1 优化css
date: 2019-04-15 11:10:04
tags: 前端优化方案
desc: 
# keywords: 
categories:
  - 前端优化方案
# from: https://bitsofco.de/the-background-properties/
# demo: ../../../demos/201703/background.html
---
### 1.1 避免使用CSS表达式
用CSS表达式动态设置CSS属性，是一种强大又危险的方式。从IE5开始支持，但从IE8起就不推荐使用了。例如，可以用CSS表达式把背景颜色设置成按小时交替的

- 尽量减少标签选择器的使用
- 尽可能少使用id选择器，多使用样式选择器(通用性强)
- 减少选择器前缀，例如.headerBox .nav .left a{} 选择器是从右向左查询的
- 避免使用css表达式

```css
background-color: expression( (new Date()).getHours()%2 ? "#B8D4FF" : "#F08A00" );
```

<a name="cdf0508c"></a>
### 1.2 减少页面中的冗余代码
尽可能提高方法的重复使用率：“低耦合高内聚”

<a name="a5919800"></a>
### 1.3 选择<link>舍弃@import
> 前面提到了一个最佳实践：为了实现逐步渲染，CSS应该放在顶部。
> 在IE中用`@import`与在底部用`<link>`效果一样，所以最好不要用它。


<a name="545e9579"></a>
### 1.4 避免使用滤镜
IE专有的`AlphaImageLoader`滤镜可以用来修复IE7之前的版本中半透明PNG图片的问题。在图片加载过程中，这个滤镜会阻塞渲染，卡住浏览器，还会增加内存消耗而且是被应用到每个元素的，而不是每个图片，所以会存在一大堆问题。<br />最好的方法是干脆不要用`AlphaImageLoader`，而优雅地降级到用在IE中支持性很好的PNG8图片来代替。如果非要用`AlphaImageLoader`，应该用下划线hack：`_filter`来避免影响IE7及更高版本的用户。
<a name="d41d8cd9"></a>
### 
<a name="c066b667"></a>
### 1.5 把样式表放在顶部

把样式表放到文档的HEAD部分能让页面看起来加载地更快。这是因为把样式表放在head里能让页面逐步渲染。<br />　　关注性能的前端工程师想让页面逐步渲染。也就是说，我们想让浏览器尽快显示已有内容，这在页面上有一大堆内容或者用户网速很慢时显得尤为重要。给用户显示反馈（比如进度指标）的重要性已经被广泛研究过，并且被记录下来了。在我们的例子中，HTML页面就是进度指标！当浏览器逐渐加载页面头部，导航条，顶部logo等等内容的时候，这些都被正在等待页面加载的用户当作反馈，能够提高整体用户体验。

<a name="517c6177"></a>
### 1.6 压缩 css

-  使用在线网站进行压缩
-  使用html-minifier 对html 中的css 进行压缩<br />
-  使用clean-css 对css进行压缩
- webpack,gulp打包工具
