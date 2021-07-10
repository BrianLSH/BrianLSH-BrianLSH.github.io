---
title: Vue生命周期
tags: Vue 基础知识 生命周期
date: 2015-08-15
toc: true
categories:
- [Vue, 基础]
---

### 关于Vue生命周期

```js
(2+) beforeCreate created beforeMount mounted 
beforeUpdate updated beforeDestroy destroyed 

*****使用了 keep-alive 就会多2个生命周期： activated deactivated****
```

### 生命周期总结

```php

beforeCreate ：vue实例的挂载元素$el和数据对象data都为undefined，还未初始化。
 
created ： vue实例的数据对象data有了，但是$el还是没有 
载入前/后 beforeMount : vue实例的$el和data都初始化了,
但还是挂载之前为虚拟dom节点，data.msg还未替换。 

mounted : vue实例挂载完成,data.msg成功渲染

更新前/后 当data变化时，会触发：beforeUpdate、updated 

销毁前/后 当销毁的时候，会触发： beforeDestroy、destroyed 

----->DOM 渲染在哪个周期中就已经完成 ： mounted
```


### 文档解读
```js
生命周期函数,就是vue在某一个时间点会自动执行的函数

beforemount------>>模板和数据相结合，即将挂载到页面之前的一瞬间
(页面还没有被渲染)

mounted------>>beforemount执行之后，模板结合数据生成的dom元素会被
挂载到页面上,也就是hello显示到页面之上,此时页面挂载后，会调用mounted， 
页面已经被渲染完毕了.

before update------>>当数据发生改变,还没有重新渲染之前，会调用 before update
updated------>>数据改变之后,会调用 updated

组件即将销毁 beforedestroy
组件实例被销毁之后，destroied
```