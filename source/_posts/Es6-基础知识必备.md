---
title: Es6--工作用到的
date: 2019-05-20
toc: true
tags: Es6 基础  
categories:
- [Es6, 基础]
---
### 廖雪峰Es6
https://es6.ruanyifeng.com/#docs/symbol
### let const 声明变量

### 解构赋值

#### 数组的结构
#### 对象的结构
#### 字符串函数结构

### 模板字符串

### 默认参数

### 展开运算符

#### 展开数组
#### 剩余参数

### 箭头函数

### 对象字面量简写法
#### 当属性与值的变量同名时。
```js
let type = 'quartz';
let color = 'rose';
let carat = 21.29;
//es5
const gemstone = {
  type: type,
  color: color,
  carat: carat
//es6
const gemstone = {type,color,carat};

console.log(gemstone);
```
#### 简写方法的名称
```js
let gemstone = {
    testFunc() {
        console.log("对象字面量方法简写");
    }
};
gemstone.testFunc();
```

#### 在对象字面量中可以使用中括号作为属性，表示属性也能是一个变量
```js
const name = 'Jane';
const person = {
  [name]: true   //'Jane':true
}
console.log(person.Jane);   //true
```

### Class类
```js
```

### 类的继承extends
```js
```

### Set和Map
```js
```

### 字符串新方法
```js
```
### 数组新方法
```js
```

### 模块
```js
```

```js
```
```js
```

```js
```
```js
```

```js
```
```js
```

```js
```
```js
```





