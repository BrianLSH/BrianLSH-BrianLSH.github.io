---
title: CLass
tags: Es6 基础  class
date: 2018-03-29
toc: true
categories:
- [Es6, 基础]
---

### class
#### 总结
```js
super 总结
总结：super调用父类的属性和方法，那么查找属性和方法的原则就近原则**

如果子类不写东西，那么直接继承父类就可以用 

但是如果子类有自己的构造函数和父类同名的方法，此时不可以直接用父类的东西，需要用super调用父类的方法和构造函数
```

#### class的创建

```js
class Star {
};

var ldh = new Star();
```


#### constructor构造函数

```js

class Star {
	constructor (uname,age){
		this.uname = uname;
		this.age = age;
	}
}
注意：类里面的方法不带function，直接写既可

类里面要有属性方法，属性方法要是想放到类里面，我们用constructor构造器

构造函数作用：接收参数，返回实例对象，new的时候主动执行，主要放一些公共的属性

constructor() 方法是类的构造函数(默认方法)，用于传递参数,返回实例对象，
通过new命令生成对象实例时，自动调用该方法。

注意：每个类里面一定有构造函数，如果没有显示定义, 
类内部会自动给我们创建一个constructor() ，

注意：this代表当前实力化对象，谁new就代表谁
```


#### class中的extends

```js
class Father {}

​class Son extends Father{}
```


#### class中的supper

```js
我们应用的过程中会遇到父类子类都有的属性，此时，没必要再写一次，
可以直接调用父类的方法就可以了

<u>super关键字用于访问和调用对象父类上的函数。可以调用父类的构造函数，
也可以调用父类的普通函数</u>

当子类没有constructor的时候可以随意用父类的，但是如果子类也含有的话，
constructor会返回实例，
this的指向不同，不可以再直接使用父类的东西

调用父类构造函
class F { constructor(name, age){} }

class S extends F { constructor (name, age) { super(name,age); } }

注意: 子类在构造函数中使用super, 必须放到this 前面(必须先调用父类的构造方法,在使用子类构造方法


调用父类普通函数
class F { constructor(name, age){} say () {} }

class S extends F { constructor (name, age) { super(name,age); } say () { super.say() } }

注意：如果子类也有相同的方法，优先指向子类，就近原则

总结：super调用父类的属性和方法，那么查找属性和方法的原则就近原则**

如果子类不写东西，那么直接继承父类就可以用 

但是如果子类有自己的构造函数和父类同名的方法，此时不可以直接用父类的东西，需要用super调用父类的方法和构造函数

		
		// class Star {}
		
		class Father {

			constructor (uname, age) {
				this.uname = uname;
				this.age = age;
			}

			qian () {
				console.log('一个亿');
			}

		}



		// 让Son类继承Father
		class Son extends Father {
			constructor (uname, age, score) {
				// 因为父类的this指向父类的实例对象
				// 子类的this指向子类的实例对象，
				// this指向不同，所以会报错
				// this.uname = uname;
				// this.age = age
				// 在this之前调用父类的里面内容
				super(uname, age);
				this.score = score;
			}

			chang () {
				console.log('唱');
			}

			qian () {
				// super可以调用父类里面的方法
				super.qian();
				console.log('转了两块钱');
			}
		}


		// 类
		var obj = new Son('儿子', 22, 99);
		console.log(obj);
		// obj.chang();
		// 子类父类同名方法, 此时就近原则直接找到子类的qian()方法, 
		//在此方法内super.qian()调用父类的方法  如果子类中没有qian()方法,则会直接调用父类的qian()方法
		obj.qian(); 

```

#### class中的this

```js
```


#### class中的this

```js
```


#### class中的this

```js
```



#### class中的this

```js
```


#### class中的this

```js
```


#### class中的this

```js
```


#### class中的this

```js
```


#### class中的this

```js
```