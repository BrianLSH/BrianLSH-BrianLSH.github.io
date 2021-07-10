---
title: JavaScript-面向对象
toc: true
tags: JavaScript 基础知识 面向对象 对象创建
date: 2018-10-25
categories:
- [JavaScript, 基础]
---

### JS面向对对象
##### Object 构造函数模式
```js


    套路：先创建空object对象，再动态添加属性方法
    适用场景：其初时候不确定对象内部数据
    
    js 内置对象 
    var obj = new Obj(); obj.name = 张三
    问题： 语句太多
    
    var obj = new Obj();
    obj.name = '张三'
    obj.age = 40
    obj.setName = function(){
        this.name = name
    }
    
    console.log(obj.name, obj.age)
 ```   
#### 对象字面量模式
 ```js
    使用{}创建对象，同时指定属性/方法
    适用场景：起始时对象内部数据是确定的
    问题：如果创建多个对象，有重复代码
    var obj = {
        name: 'jack',
        age: 30,
        setName: function(){
            this.name = name
        }
    }
    
    obj.setName('hanmeimei')
    console.log(obj)

 ```
#### 工厂模式
 ```js
通过工厂函数动态创建对象并返回
适用场景：需要创建多个对象
问题：对象没有一个具体的类型，都是Object类型
function createTeacher(name,age,major){

    var obj = {
           name:name,
            age:age,
            major:major,
            setName: function(name){
                this.name= name
            } 
    }
    
    return obj;
}

var p1 = createPerson('zhangsna', 30, 'it');
var p2 = createPerson('lisi', 45, 'trade');

function createStudent(name,age,major){

    var obj = {
           name:name,
            age:age,
            major:major,
            setName: function(name){
                this.name= name
            } 
    }
    
    return obj;
}

只知道创造了一个对象 无法判断 对象之间的区别 属于学生还是teacher
 ```
#### 自定义构造函数模式
 ```js
套路：自定义构造函数，通过new创建对象
适用场景：需要创建多个类型确定的对象
问题：每个对象都有相同的数据，浪费内存

function Student(name, age, major){
     name:name,
            age:age,
            major:major,
            setName: function(name){
                this.name= name
            } 
}


function Teacher(name, age, major){
     name:name,
            age:age,
            major:major,
            setName: function(name){
                this.name= name
            } 
}

var p1 = new Student('zang', 30, 'dazhuan');
var t1 = new Teacher('xiaoli', 40, 'qinghua'); 
每个实例都有相同的 属性方法，造成内存的浪费
 ```
#### 构造函数 + 原型 的组合模式
 ```js
自定义构造函数，属性在函数中初始化，方法添加到原型上

适用场景：需要创建多个类型确定的对象

```

```php
函数原型 ==> Obj ===> null
```

