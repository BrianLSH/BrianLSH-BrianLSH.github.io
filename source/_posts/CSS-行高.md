---
title: CSS行高设置
toc: true
tags: CSS基础 行高
date: 2015-04-09
categories:
  - [CSS, 基础]
---

### 行内元素没有行高
html 行内元素是没有宽高的！也就是说没有width！高的话可以用line-height撑起来。

要想行内元素有宽高，可以将行内元素转化为块级元素或者行内块元素

用block或者inline-block 块或者行内块元素，一个独占一行，一个不独占一行, 
调行高， line-height 

padding-top 是要算在高度里面的导致边长，margin-top能改变高度，但是还会导致整体移动。
vertical-align可以调整行内块的属性或者具体的值。
基线对齐 主要用于行内块元素

设置float浮动会隐式修改元素的display为block 设置宽高