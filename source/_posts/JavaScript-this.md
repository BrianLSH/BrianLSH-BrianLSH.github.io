---
title: JavaScript-this
toc: true
tags: JavaScript 基础知识 this
date: 2018-03-25
categories:
- [JavaScript, 基础]
---

### this常见问题

#### 概念问题
```css
执行上下文是执行的环境
this叫做执行主体，是谁把他执行,所以他们两个不一回事。

如何区分执行主体:
和函数在那里执行和创建没有必然的关系一般我们提到this, 都是函数中的
this, 不然全局中输出this === window

我们所说的this是指函数中的this, 那我们如何区分执行主体,和函数在哪里执行创建
没有必然的关系
首先我们看函数前面是否有点,有点,他前面是谁this就是谁,没有点，this
就是 window(非严格模式)/undefined(严格模式)
--- 自执行函数this 一般是指window或者undefined
--- 回调函数this一般也是thih或者undeifend(除非某个函数内部给回调函数做了
特殊处理，这样函数中的this有自己的特殊处理)
--- 给当前元素的某个事件行为绑定方法, 当事件触发,方法中的this就是当前操作的
元素,（特殊 ie 678基于dom2时间绑定attachevent 方法中的this不是元素）
箭头函数中（私有块级上下文）没有自己的this,所用到的this 都是期上下级上下文中的this
（也就是说没有初始化this这一步）

```
#### 什么时间能确定this
```
this的指向在函数定义的时候是确定不了的，只有当函数执行的时候，
才知道this到底指向谁，实际上this最终的指向是那个调用它的对象。
```
#### 普通函数中的This

```js
this最终指向的是调用它的对象


function fn(){
    var user = "hunt_bo";
    console.log(this.user); //undefined
    console.log(this); //Window
}
fn();
这时候的this指向全局对象window。


下面的代码就可以证明。和上边是一样的效果，区别就是我们定义的一些变量函数，
其实是在给window添加属性。
function fn(){
    var user = "hunt_bo";
    console.log(this.user); //undefined
    console.log(this);　　//Window
}
window.fn();
```

#### 构造函数中的This
```js
function Person(age, name) {
    this.age = age;
    this.name = name
    console.log(this)  // 此处this分别指向Person的实例对象p1和p2
}
var p1 = new Person(15, '张三')
var p2 = new Person(18, '李四')
在构造函数中，它的this始终指向构造函数构造出来的实例，结合前面所分享的原型里边的知识，
在构造函数中直接打印this.__proto__.constructor，就会直接打印构造函数自己，
有兴趣的话可以试一下。
```

#### 对象方法中的This
```js
var obj = {
     fn: function () {
         console.log(this); // obj
     }
}
obj.fn();
对象方法调用的时候， 此时this指向该方法所属的对象，就是说fn是obj的一个方法，
那么当通过obj.fn调用的时候，方法中的this指向的是obj对象。
```

#### 事件绑定中的This
```js
<body>
    <button id="btn">text</button>
<script>
    var oBtn = document.getElementById("btn");
    oBtn.onclick = function() {
        console.log(this);
    }
</script>
</body>
在事件绑定中的this，指向的是绑定事件的对象，就是说this指向button
```

#### 定时器中的this
```js
setInterval(
    function(){ 
        console.log(this); //window
    }, 
3000);
定时器中的this指向的是window，这个就不做过多的解释了。
```

#### 箭头函数中的this
```js
箭头函数中的this指向的是定义时的this，而不是执行时的this，说白了就是箭头函数
是没有this，this指向谁主要取决于箭头函数所处的环境，箭头函数中的this指向外部
环境中的this指向。虽然有些拗口，但是应该还是很好理解的。
```
#### 类class中的this

```js
创建类：class 类名 {}

​	属性：constructor：class 类名 {constructor () {}}

​	方法：class 类名 {constructor () {} sing () {}}
​	对类实例化会返回对象：new Star()

​	继承：exnteds，重复：super调用父类的构造函数和普通函数

​	this指向：构造函数this指向当前实例对象，在方法里面this指向调用者
```
#### 改变this的指向
```js
改变this的指向的方法主要有call，apply，bind

.call(),  call(thisScope, arg1, arg2, arg3...)
 
.apply(), apply(thisScope, [arg1, arg2, arg3...]);两个参数
 
.bind()  bind(thisScope, arg1, arg2, arg3...)
```


#### 小技巧

```css
看有没有点, 有点的谁调用属于谁, 没有点就是window的
执行主体是谁 跟在哪里调用的没有关系,要看谁谁调用的。
```