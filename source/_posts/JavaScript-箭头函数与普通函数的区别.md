---
title: JavaScript-箭头函数与普通函数的区别
toc: true
tags: JavaScript 基础知识 函数 箭头函数
date: 2019-08-25
categories:
  - [JavaScript, 基础]
---

### 箭头函数与普通函数的区别

```
- 内部没有arguments
- 内部没有this
- 不能作为构造器
```

#### 写法区别

```js

es5 写法

var show = function (x) {
    return 'es5'
}

es6写法 show是变量

let show = (x) => {
    return 'es6'
}

唯且仅有只有一个参数的时候()可以省略

let show = x => return {
    'es6'
}

当只有return一行的时候，可以省略return，{}

let add = (a,b) => a+b

```

#### 函数参数不确定

```js

es5 写法

arguments是伪数组，转化为数组，Array.from(arguments)或者
Array.prototype.slice.apply(arguments)，将他转化数组
function show() {
    console.log(arguments)
}

es6写法

  function show(...arg){
      console.log(arg);//arg是一个数组
  }
  or

  let show = (...arg)=> console.log(arg)

```

#### 函数值默认

```js
let show(a, b=1, c=3) => console.log(a+b+c)

show(0); //3
show(0,2) //4
show(0,2,3) //5
```

#### 小例子

```js

例子一:
function m() {
    return function(n){
        return m+n
    }
}

箭头函数写法

let m => n => m+n 非常简洁

```

#### 遗留问题

```js
什么是函数柯里化
```
