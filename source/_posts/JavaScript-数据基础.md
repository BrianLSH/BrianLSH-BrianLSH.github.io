---
title: JavaScript-基础
toc: true
tags: JavaScript 基础知识 数据类型
date: 2015-03-25
categories:
- [JavaScript, 基础]
---

###  js 基础知识及原理

#### ES 6为止,7种类型

```js
值类型(基本类型)：字符串（String）、数字(Number)、
布尔(Boolean)、对空（Null）、未定义（Undefined）、Symbol。

引用数据类型：对象(Object)、数组(Array)、函数(Function)。
```

```js
数值（number）：整数和小数（比如1和2.2）
字符串（string）：文本（比如Everybody Loves Eileen）。
布尔值（boolean）：表示真伪的两个特殊值，即true（真）和false（假）
undefined：表示“未定义”或不存在，即由于目前没有定义，所以此处暂时没有任何值
null：表示空值，即此处的值为空
对象（object）：各种值组成的集合
Symbol：独一无二的值，可以保证不会与其他属性名产生冲突
```

#### 内置的类型识别方法

```js
typeof 运算符
instanceof 运算符
Object.prototype.toString.call() 
```

#### 堆和栈
```js
值类型：
string number boolean null  undefined  
简单数据类型 存放的栈区(栈内存、变量对象), 属性名=属性值

引用类型
数组、对象、函数
对象 属性名=内存地址，指向堆区，堆内存空间

两种类型的复制与传递
值类型相当于copy, 互不影响, 引用类型操作的是指向内存的地址,相互影响
函数参数的引用传递及值传递,如果实参是值类型,会复制一个值类型的副本给函数,
不会影响原来的传递参数
如果是 引用类型,传递只是引用类型的一个地址值,在函数内部操作参数对应的
引用对象会影响到传递的参数

```

#### 事件循环机制EventLoop
```css
javascript 代码是队列的形式一个个进行执行的,同一时间只能执行一段代码

队列数据结构:
js单线程,
为什么是单线程？ 执行线程和ui现成互斥
同步任务 赋值操作、循环、分支语句等
异步任务: dom事件、ajax、bom的一下api

js事件循环机制：
---js的执行引擎的主线程从任务队列中获取任务执行
---如果任务是异步的,那么运行到异步任务时,异步任务就退出主线程,主线程进行下一个任务的获取处理
---如果异步任务完成, 就插入到任务队列的末尾,等待主线程处理

```
#### 执行上下文(函数)

##### 栈的数据结构
```css
栈的数据结构:先进后出 栈顶push 栈低pop
EC:函数执行环境(或者执行上下文) Execution Context
ECS: 执行环境栈 Execution Context Stack
Vo变量对象:
scope chain 作用域链
```
##### 执行上下文的执行栈
```js
js执行在单线程上,所有的代码都是排队执行

一开始浏览器执行全局的代码时,首先创建全局的执行上下文,压入执行栈的顶部

每当进入一个函数的执行,就会创建函数的执行上下文,并且把它压入执行栈的顶部,
当前函数执行完成后,当前函数的执行上下文出栈,并等待垃圾回收

浏览器的js执行引擎总是访问栈顶的执行上下文
全局上下文只有唯一的一个,他在浏览器关闭时候出栈
```
##### 执行栈的压栈出栈过程:
```js
四个函数f1  f2->f3->f4    f1()  f2()
f1的EC-->压入执行环境栈
f2的EC->压入执行环境栈  在f1之上
f3的EC->压入执行环境栈, f2之上
f4的EC->压入执行环境栈, f3之上

f1执行完成-> f1的ec出栈
f4执行完成-> f4的ec出栈
f3执行完成-> f3的ec出栈
f2执行完成-> f2的ec出栈

进栈 1234  出栈 4321

最后只剩下全局的EC 浏览器关闭出栈
```
##### 执行栈的压栈出栈过程:
```js
创建---->执行---->销毁

创建：生成变量对象  建立作用域链   确定this指向
执行: 变量赋值  函数引用   执行其他代码
执行完毕, 等待垃圾回收你
```

### 函数的作用域

#### js的解释和执行阶段
```css
解释: 词法分析,语法分析,作用域规则确定
执行阶段:创建执行上下文, 执行函数代码, 垃圾回收
```

#### 作用域

```js
作用域: 变量声明的区域 也就是变量和函数的可访问范围

函数的参数 只能在内部访问，局部变量
没有 var  全局 任何地方可以访问
```
#### 变量提升
#### 作用域链
```js
作用域链是一个数组,由内向外逐级查找,直到找到同名标识符,找到不在遍历,找不到报错
```

### 垃圾回收机器
### 原型链

不确定参数  处理 最大最小值
参数太多怎么办？ 封装成一个对象传递

### 常用数组方法

```js
Array.map()

此方法是将数组中的每个元素调用一个提供的函数，结果作为一个新的数组返回，并没有改变原来的数组
let arr = [1, 2, 3, 4, 5]
    let newArr = arr.map(x => x*2)
    //arr= [1, 2, 3, 4, 5]   原数组保持不变
    //newArr = [2, 4, 6, 8, 10] 返回新数组
　　

Array.forEach()

此方法是将数组中的每个元素执行传进提供的函数，没有返回值，注意和map方法区分
let arr = [1, 2, 3, 4, 5]
   num.forEach(x => x*2)
   // arr = [1, 2, 3, 4, 5]  数组改变,注意和map区分
　　

Array.filter()

此方法是将所有元素进行判断，将满足条件的元素作为一个新的数组返回
let arr = [1, 2, 3, 4, 5]
    const isBigEnough = value => value >= 3
    let newArr = arr.filter(isBigEnough )
    //newNum = [3, 4, 5] 满足条件的元素返回为一个新的数组
　　

Array.every()

此方法是将所有元素进行判断返回一个布尔值，如果所有元素都满足判断条件，则返回true，否则为false：
let arr = [1, 2, 3, 4, 5]
    const isLessThan4 = value => value < 4
    const isLessThan6 => value => value < 6
    arr.every(isLessThan4 ) //false
    arr.every(isLessThan6 ) //true
　　

Array.some()

 此方法是将所有元素进行判断返回一个布尔值，如果存在元素都满足判断条件，则返回true，若所有元素都不满足判断条件，则返回false：
let arr= [1, 2, 3, 4, 5]
    const isLessThan4 = value => value < 4
    const isLessThan6 = value => value > 6
    arr.some(isLessThan4 ) //true
    arr.some(isLessThan6 ) //false
　　

Array.reduce()

 此方法是所有元素调用返回函数，返回值为最后结果,传入的值必须是函数类型：
let arr = [1, 2, 3, 4, 5]
   const add = (a, b) => a + b
   let sum = arr.reduce(add)
   //sum = 15  相当于累加的效果
   与之相对应的还有一个 Array.reduceRight() 方法，区别是这个是从右向左操作的
　　

Array.push()

 此方法是在数组的后面添加新加元素，此方法改变了数组的长度：
   
Array.pop()

 此方法在数组后面删除最后一个元素，并返回数组，此方法改变了数组的长度：
let arr = [1, 2, 3, 4, 5]
    arr.pop()
    console.log(arr) //[1, 2, 3, 4]
    console.log(arr.length) //4
　　

Array.shift()

 此方法在数组后面删除第一个元素，并返回数组，此方法改变了数组的长度：
let arr = [1, 2, 3, 4, 5]
    arr.shift()
    console.log(arr) //[2, 3, 4, 5]
    console.log(arr.length) //4 
　　

Array.unshift()

 此方法是将一个或多个元素添加到数组的开头，并返回新数组的长度：
let arr = [1, 2, 3, 4, 5]
    arr.unshift(6, 7)
    console.log(arr) //[6, 7, 1, 2, 3, 4, 5]
    console.log(arr.length) //7 
　　

Array.isArray()

 判断一个对象是不是数组，返回的是布尔值
 
Array.concat()

 此方法是一个可以将多个数组拼接成一个数组：
let arr1 = [1, 2, 3]
      arr2 = [4, 5]
  let arr = arr1.concat(arr2)
  console.log(arr)//[1, 2, 3, 4, 5]
　　

Array.toString()

 此方法将数组转化为字符串：
let arr = [1, 2, 3, 4, 5];
   let str = arr.toString()
   console.log(str)// 1,2,3,4,5
　　

Array.join()

  此方法也是将数组转化为字符串：
let arr = [1, 2, 3, 4, 5];
   let str1 = arr.toString()
   let str2 = arr.toString(',')
   let str3 = arr.toString('##')
   console.log(str1)// 12345
   console.log(str2)// 1,2,3,4,5
   console.log(str3)// 1##2##3##4##5
　　

通过例子可以看出和toString的区别，可以设置元素之间的间隔~ 

Array.splice(开始位置， 删除的个数，元素)万能方法，可以实现增删改：

let arr = [1, 2, 3, 4, 5];
     let arr1 = arr.splice(2, 0 'haha')
     let arr2 = arr.splice(2, 3)
     let arr1 = arr.splice(2, 1 'haha')
     console.log(arr1) //[1, 2, 'haha', 3, 4, 5]新增一个元素
     console.log(arr2) //[1, 2] 删除三个元素
     console.log(arr3) //[1, 2, 'haha', 4, 5] 替换一个元素
```

### 常用字符串方法
#### 背啊背我骄傲的心
```css
字符串方法
 拼接 concat
 截取 
str.slice(1, 5) 1-5之间 
str.substring(1,5) 包含第一个 不包含最后一个
str.substr(2, 6);//从下标2开始往后数6个数 不包括第一个下标
str.indexOf("abc") 含返回第一位的下标，停止查找，如没有返回 -1
str.lastIndexOf("abc") 含返回第一位的下标，停止查找，如没有返回 -1
大小写转换  toUpperCase  toLowerCase
重复字符串 repeat
字符串转数组 split()
字符串查找   
charAt  返回指定位置的字符串
str.replace("天天", "**"); 只替换一次  
str.match("天天"); 返回查找到的字符串  没有 null
str.search("天天") 找到返回下标 找不到返回 -1
str.startsWith("he"); 以he开始   布尔值
str.endsWith("world"); 以world 结束 布尔值
str.includes("o");  布尔值
```

```js
charAt()

查找返回指定位置的字符

 

 var str = "abcdefg";
        var s = str.charAt(5); // 下标为5的字符
        console.log(s);//f
 

charcodeAt()

查找返回指定位置字符的unicdoe码

 var str = "abcdefg";
        var s = str.charCodeAt(5); // 下标为5的字符的unicdoe码 
        console.log(s);//102
concat()

连接字符串

 

 var str = "abc";
        var str1 = str.concat("a", "b", "c", "dsdafsdafsad");
        console.log(str1);//abcabcdsdafsdafsad
 

slice()

字符串截取

 

var str = "abcdefghijklm";
        var str1 = str.slice(1, 5);
        console.log(str1);//bcde
 

详细用法请参考数组用法。

split()

将字符串转换为数组

 

 var str = "abcdefg"
        var str1 =str.split("")
        console.log(str);//abcdefg
        console.log(str1)//["a", "b", "c", "d", "e", "f", "g"]
 

substring()

字符串截取

 

 var str = "abcdefghijklm";
        var str1 = str.substring(1, 9);//从下边1开始到下边9结束不包括下标9那一项
        var str2 = str.substring(9, 1);
        console.log(str1);//bcdefghi
        console.log(str2);//bcdefghi
 

substr()

字符串截取

 

var str = "abcdefghijklm";
        var str1 = str.substr(2, 6);//从下标2开始往后数6个数
        console.log(str1);//cdefgh
 

indexOf()

遍历字符串

查找包含第一个参数的字符串，如包含返回第一位的下标，停止查找，如没有返回 -1。第二个参数表示从此下标开始查找。

 

 var str = "abcdefabcjklm";
        var a = str.indexOf("abc")
        var b = str.indexOf("abc", 1);
        console.log(a);//0
        console.log(b);//6
 

toUpperCase

转大写

var str = "aAbBcCdD";
        console.log(str.toUpperCase());//AABBCCDD
toLowerCase

转小写

 var str = "aAbBcCdD";
         console.log(str.toLowerCase());//aabbccdd
replace()

替换字符串

只能匹配一次

 

var str = "今天天天天气好好";
        var str1 = str.replace("天天", "**");
        console.log(str1);//今**天天气好好
        
 

match()

查找字符串

 

 var str = "今天天气好好";
        var result = str.match("天天");
        console.log(result);//["天天", index: 1, input: "今天天气好好", groups: undefined]
 

search()

查找字符串返回下标

var str = "今天天气天天好好";
        var result = str.search("天天");
        console.log(result);//1
 startsWith  

判定一个字符串是否以另一个字符串开头
 
复制代码
   var str = "hello world";
    var result = str.startsWith("he");
   console.log(result)//true
   //当为两个参数时，第二个表示开始位数。
    var result = str.startsWith("he",1);
     console.log(result)//flase
复制代码
endsWith

判定一个字符串是否以另一个字符串结尾
复制代码
  var str = "hello world";
        //检测尾部
        var result = str.endsWith("world");
        console.log(result);//true
        //检测指定位置是否以指定字符结尾
        var result1 = str.endsWith("wo", 8);
        console.log(result1)//true
复制代码
includes

检测是否包含指定字符串

 var str = "hello world";
        var result = str.includes("o");
        console.log(result);//true
        var result1 = str.includes("o", 8);
        console.log(result1);//false
 repeat

 重复字符串

var str ="haha"
    var str1 = str.repeat(3);
    console.log(str1)//hahahahahaha
```