---
title: Bom-Dom
toc: true
tags: JavaScript Bom Dom
date: 2017-03-20
categories:
- [JavaScript, 基础]
---

### Client家族

```css
1、client概述
对象.clientWidth/clientHeight 和我们offsetWidth/offsetHeight 最大的区别就是不包含边框；
但是也包含padding;且数值不带单位。

1）对象.clientWidth/clientHeight -- 返回自身包含padding+内容 的大小(值不带单位！) -- 不含边框。
2）对象. clientTop --- 返回元素上边框的大小 (注意！没有clientBottom)
3）对象.clientLeft --- 返回元素左边框大小 (注意！没有clientRight)
注 （1）client 可读不可写属性
（2）获取的值不带单位
（3）边框大小如何获取 clientLeft/Top
（4）获取的宽高是否包含边框（border） 边距（padding）（包含padding 不包含边框）

Note:
    clientWidth/clientHeight 获取的元素的真实宽高，不随窗口大小改变而改变
```  