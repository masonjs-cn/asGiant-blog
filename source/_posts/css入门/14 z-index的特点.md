---
title: 14 z-index的特点
date: 2019-04-30 18:19:05
tags: css入门
desc: 
# keywords: 
categories:
  - css入门
# from: https://bitsofco.de/the-background-properties/
# demo: ../../../demos/201703/background.html
---

- 默认是书写顺序在后的定位元素覆盖在顺序钱的定位元素
- 可以使用z-index属性修改定位元素的层级关系
- 所有定位元素的z-index默认都是一样的
- z-index值是数字没有单位，支持负数
- 一般都是同级元素进行层级的比较
- 当参数是相对定位或绝对定位的时候，父级元素之间没有z-index值，子级元素的z-index值会出来比较。
