---
title: vue-cli项目中src目录每个文件夹和文件的用法
toc: true
tags: Vue 基础知识 路由跳转
date: 2018-06-25
categories:
- [Vue, 基础]
---

### vue-cli项目中src目录每个文件夹和文件的用法？

```C#
 src assets           |     静态资源 （图片、js、css）
 components           |     非路由组件
 views                |      路由组件
 router               |      路由配置
 store                |      vuex（仓库）
 App.vue              |      挂载的第一个组件
 main.js              |      全局的文件
 
 index.html => main.js  => App.vue
  
 ```