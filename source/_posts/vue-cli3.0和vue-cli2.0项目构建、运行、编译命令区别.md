---
title: vue-cli3.0和vue-cli2.0项目构建、运行、编译命令区别
toc: true
tags: Vue 基础  脚手架 基础 
date: 2018-04-03
categories:
- [Vue, 基础]
---

### 一、安装上区别： 

1.Vue cli 2 版本安装命令 : 
```js
    npm install -g vue-cli
```
 2.Vue cli 3 版本安装命令：
```js
    npm install -g @vue/cli
```

### 二、创建项目区别
1.Vue cli 2 版本创建项目命令 :
```js
    vue init webpack project
```
2.Vue cli 3 版本创建项目命令 : 
```js
    vue create project
```
### 三. 编译运行项目区别 
1.Vue cli 2 版本编译运行项目命令 :  
```js
    npm run dev
```
2.Vue cli 3 版本编译运行项目命令 :  
```js
    npm run serve
```
### 项目目录结构
可以明显的看出来，vue-cli2.0与3.0在目录结构方面，有明显的不同
（vue3.0我是安装了css预处理器，所以看上去内容更丰富哈）

vue-cli3.0移除了配置文件目录，config 和 build 文件夹

同时移除了 static 静态文件夹，新增了 public 文件夹，细心的你，
打开层级目录还会发现， index.html 移动到 public 中

### 配置项

vue-cli2.0的域名配置，分为开发环境和生产环境，所以配置域名时，
需要在config中的dev.env.js和prod.env.js中分别配置

前面说过，到了3.0 config文件已经被移除，但是多了.env.production和
env.development文件，除了文件位置，实际配置起来和2.0没什么不同

当然，没了config文件，跨域需要配置域名时，从config/index.js 
挪到了vue.config.js中，配置方法不变


在3.0中，vue.config.js中有关于mock的配置

要注意的是：mockjs是用来模拟产生一些虚拟的数据，方便前端在后端接口还没有开发出来时独立开发

即使使用了真实的url，但是mockjs拦截了ajax请求，返回的是设定好的本地数据

如果你想正常从后端获取数据，就要关掉mock的使用，我是直接删掉的，当然你可以选择别的办法

main.js中有一段关于mock.js的描述（注意上线前要去掉你的mock）

### 可视化界面
找到项目，vue ui 命令会直接打开可视化界面，里面可以进行配置、依赖等操作

对于不喜欢命令行的皮友可以说是非常友好了