---
title: Vue插槽详解
toc: true
date: 2015-03-26
tags: Vue  基础知识 slot插槽
categories:
- [Vue, 基础]
---



### 匿名插槽(文档中的默认插槽)

```
所谓插槽就是在子组件中定义一个slot标签,把父组件中的内容
填充过去

使用匿名插槽 会把父组件中子组件内的所有内容一次性传递过去
如果有多个slot, 就想是把所有内容copy了好几份, 一个slot
标签就是一份copy

父组件
<div>
<child>jack lily </child>
</div>

子组件
<div>
你好 <slot></slot>
</div>

此时会把jack lily会把slot标签替换掉,

```
### 插槽后备内容
```
父组件
<div>
<child>jack</child>
</div>

子组件
<div>
你好 <slot>tom</slot>
</div>

父组件中子组件内没有内容, 则子组件显示tom, 如果传入内容,
tom不显示, 就会显示jack
```
### 带名字的插槽(具名插槽)

```
匿名插槽有缺点,slot会把父组件里面的内容全部替换掉,不能针对性的
替换，所以我们也要用具名插槽, slot根据name值接收相对应的
内容，从而显示不同内容

<div>
   <child>
      <span name='header'></span>
   
      <span name='body'></span>

     </child>
</div>


<child>
    <span slot='header'>默认header</span>
    <span slot='body'>默认body</span>
</child>

带名字的插槽 针对性 传入接收
具名插槽也支持后备, 如传入显示默认内容

```

### 作用域插槽

```
让插槽内容能够访问子组件中才有的数据

自 2.6.0 起 slot-scope被废弃

通过属性绑定的方式, 把数据绑定到slot上,然后在父级作用域
通多slot-scope 得到一个对象, 是在slot上绑定的属性集合,
然后拿到我们需要的值, 然后再通过 具名插槽, 把整个内容传给
插槽,做一个回传,有一个一来一回的过程

3.0版本
还是 首先绑定属性, 我们叫做插槽 prop
父级作用域使用v-solt 获取我们需要的值, 其他同上
```