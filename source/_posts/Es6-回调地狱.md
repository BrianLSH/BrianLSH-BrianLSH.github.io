---
title: 回调地狱
date: 2018-03-20
toc: true
tags: Es6 基础  Promise 回调地狱 await async
categories:
- [Es6, 基础]
---

### 回调地狱

回调地狱其实就是异步回调里面嵌套异步回调,此次请求的参数是上次请求的结果,
多个类似这样的嵌套.

### 解决办法：await  async

await 后面跟的是promise, 他会强制把异步函数变成同步, 后面的promise结果
可以在前面用一个变量接收, 但是会造成代码阻塞,需要谨慎使用。

为了避免代码阻塞, 需要在外部父级函数加一个async, await和async配合使用

await 后面的promise只有resolve了之后才会执行后面的代码逻辑
如果要捕获reject,要在await函数外面包一层 try/catch

## async函数

es2017 引入async函数，让异步操作更加方便：写法上更接近同步。

`async`

它用来修饰一个函数，会返回一个promise对象，可以使用then方法添加回调函数。当函数执行时，如果遇到 了await就会先返回，等 到异步操作完成，再接着执行函数体后面的语句。

```javascript
function f1(){
	return 1;
}
async function f2() {
	return 2;
}

```



`await`

- 接一个promise对象， 它会自动解析这个promise对象中的promiseValue。
- 只能出现在async函数中。
- 一般在后面接一个函数，而这个函数会返回一个promise对象

如下示例：

```javascript
const fs = require('fs');
function readFile(filename) {
  return new Promise((resolve, reject) => {
    fs.readFile(filename, 'utf8', (err, data) => {
      if (err) {
          resolve(null);
      } else {
        resolve(data);
      }
    });
  });
}

async function dosomethin(){
    let rs = await readFile(); //允许promise的返回值存入变量, 异步变为同步,使代码更优雅
} 
```



