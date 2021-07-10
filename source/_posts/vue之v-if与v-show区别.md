---
title: v-if与v-show
tags: Vue 基础知识 v-if v-show
date: 2018-06-20
toc: true
categories:
- [Vue, 基础]
---

### v-if  v-show区别

```js
v-if更高的切换开销，v-show更高的渲染开销，
频繁切换 v-show比较好，运行时条件不太可能改变 v-if比较好


v-if监听组件的销毁与创建    v-if惰性，初始条件为假，什么也不做，只到条件第一次为真时候，才会开始条件渲染
v-show 不管初始条件是什么，元素总是被渲染，并且只是简单的
基于css进行切换
```