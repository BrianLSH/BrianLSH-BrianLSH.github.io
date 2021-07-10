---
title: vue-router动态路由的定义
toc: true
date: 2019-03-02 
tags: Vue 动态路由 
categories:
- [Vue, 基础]
---


### 怎么定义vue-router的动态路由 
```
在router目录下的index.js文件中，对path属性加上/:id 

怎么获取传过来的动态参数？ 

使用router对象的params.id

