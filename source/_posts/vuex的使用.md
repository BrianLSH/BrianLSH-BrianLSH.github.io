---
title: vuex的使用
tags: Vue 基础知识 VueX
date: 2017-05-15
toc: true
categories:
- [Vue, 基础]
---

### vuex原理 

```php
1. vuex其实是一个vue的插件，高度依赖vue.js 

2. vue插件都需要一个install方法， install方法调用了applyMixin，该方法主要是在所有组件中的beforeCreate中注入了this.$store对象。 

3. vue 自身的响应式设计，依赖监听、依赖收集都属于 vue 对象 Property set get 方法的代理劫持。 


常用方法
State、 Getter、Mutation 、Action、 Module

```

### VueX 的使用

```php

创建容器实例并且导出-->在main.js导入


组件中this.$store 其实就是我们导出的store实例，原因是  
Vuex自动帮我们把容器实例挂载到了Vue.prototype原型对象  
中了，所以我们在哪里都可以用 
```

### state(容器的状态)

```php

state->类似于组件中的data，简单理解就是需要把共享的数据
初始化到state中
state->访问->this.$store.state.xxx 模板中$store.state.xxx

**************************************
**************************************
**************************************
```
### mutation(只能同步，直接更改状态)

```js
mutations(修改容器的方法)
mutations 类似于methods  主要用来修改state  
mutations中没有this
mutations 函数的第一个参数是state

 mutations: {
    setUser (state, data) {
      state.user = data
    }
  
方法中调用->this.$store.commit('mutation函数名', 可选参数)
组件中调用->$store.commit('函数名',可选参数)

注意：
   修改state只能通过修改mutations，不能直接修改state数据 调试工具只记录mutations的提交
  
   mutations 传参  传过个 可以传对象过去
   
   不能再muations中执行异步操作，修改state，调试工具出问题
   
**************************************
**************************************
************************************** 
 ```
 ### Action -->作用 定义  调用  
```php
action 类似于mutation 不同的是把异步操作写到action也不要  
在action中修改state，action 中异步操作结束以后，提交 mutation 来修改 state
action 函数的第 1 个参数是容器对象
action 也可以像 mutation 函数一样自定义传参

使用
视图=>@click="$store.dispatch('action函数名'，可选参数)"
方法==>this.$store.dispatch('action函数名'，可选参数)

action里面函数第一个参数默认接受store实例，用store.commit提交
在mutation里面，函数第一个参数默认state

**************************************
**************************************
************************************** 
异步
在试图上做分发($store.dispatch)，在action里面commit 提交mutation (store.commit)，在mutation里面修改state

```

