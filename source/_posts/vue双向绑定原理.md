---
title: vue双向绑定原理
toc: true
date: 2019-02-15
tags: Vue 双向绑定
categories:
- [Vue, 基础]
---
### Vue的双向数据绑定原理是什么？ 
```php
view 更新data 可以通过事件监听，关键 data 如何更新view呢？

通过Object.defineProperty()对属性设置一个set函数，当数据改变了，就会  
触发这个函数，所以只要将一些需要更新的方法放在这里面，就能实现data更新view了   


1. 实现一个监听器Observer，用来劫持监听所有属性，如果有变动，通知订阅者
2. 实现一个订阅者watcher，可以收到属性的变化通知并执行相应的函数，从而更新视图   
3. 实现一个解析器Compile，可以扫描和解析每个节点相关指令，初始化末班数据以及初始化相应的订阅者

监听器 observer ===》 订阅者 watcher

Compile 解析器 ===解析相关指令===》wachter 

watcher ===更新===》view
 
```

```js
总计：vue数据双向绑定是通过数据劫持结合发布者-订阅者模式的方式来实现的。

 1.为什么会多出这两个方法呢？ 因为vue是通过Object.defineProperty()来实现数据劫持的。

 2.Object.defineProperty( )是用来做什么的？ 它可以来控制一个对象属性的一些特有操作，
比如读写权、是否可以枚举，这里我们主要先来研究下它对应的两个描述属性get和set。
 Object.defineProperty(对象,属性,{ get(){}, set(){} })
 
 ```