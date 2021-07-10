---
title: vue路由传参及跳转
toc: true
tags: Vue 基础知识 路由跳转
date: 2017-05-19
categories:
- [Vue, 基础]
---

### 路由传参

#### 动态路由传参
```js
路由中 path: '/usr/:id'

获取参数 $route.params.id
```

#### props 设置为true
```js
在组件中定义同名的参数属性,
特点：不依赖于任何路由组件规则，达到了解耦的状态

path: '/usr/:id'

页面中{{id}}直接使用
props: ["id"]
```

### 路由的跳转方式

#### 声明式导航

```js
<router-link :to='..'>
```

#### js控制编程式导航

```js
//当前路由的view跳转到 /home
this.$router.push('home')

// 对象  当前路由跳转到 /home
this.$router.push({path: 'home'})

//命名路由
this.$router.push({name: 'product', params: {productId: 123}})

//有查询参数的路由， 变成 /register? type=stu
this.$router.push({path: 'product', query: {productId: 123}})

/*
如果提供了path params 会被忽略，上述例子中query并不属于这种情况，
取而代之的是下面的做法，你需要提供路由的 name 或者手写完整的
带有路由的 path
*/

const userId = 123
router.push({name:'user',params: {userId}})  // /user/123
router.push({path: `/user/${userId}`})  // /user/123

// 这里的params不生效
router.push({path: '/user', params: {userId}})  // /user

2. this.$router.xxx push() ： history添加一个记录 replace() ： history不会记录上  go() ==>正整数 或者 负数
```

### 路由嵌套

#### 
```js
首先在组件中提供组件出口, router-view
路由中使用children属性
```

### 命名视图
```js
可以有多个router-view

使用场景  先做好布局，不同的组件放不同的内容
参考：老马VueRouter与VueX详解
```

### 路由的三种守卫
