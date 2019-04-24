---
title: JavaScript系列之原型与原型链
date: 2019-4-20 10:47:35
categories: js
tags: js
---

## 前言

在JavaScript语言中实际上并不存在“类”，那么它是如何实现**继承**、**多态**、**实例化**等特性呢。它采用了与类不同的另一种技术，将其称之为**原型**，并通过**原型链**来实现**继承**、**多态**等特性。

但是需要注意的是JavaScript的**继承**,与Java的继承实际上有很大的区别，在Java语言中，**继承**是一个**拷贝过程**在物理地址上发生了拷贝，而JavaScript语言是通过**原型链**将其"链接"在一起，没有发生实际的拷贝。

<div><!--more--></div>

## 构造函数创建对象

```
function Person() {

}
var person = new Person();
person.name = 'Kevin';
console.log(person.name) // Kevin
```

在这个例子中，Person 就是一个构造函数，我们使用 new 创建了一个实例对象 person。
## 原型

### prototype

什么是原型呢？可以这样理解：每一个JavaScript对象(null除外)在创建的时候就会与之**关联**另一个对象，这个对象就是我们所说的**原型**，每一个对象都会从**原型**"**继承**"属性。


```
function Person() {

}
// 虽然写在注释里，但是你要注意：
// prototype是函数才会有的属性
Person.prototype.name = 'Kevin';
var person1 = new Person();
var person2 = new Person();
console.log(person1.name) // Kevin
console.log(person2.name) // Kevin
```

这个函数的 prototype 属性到底指向的是什么呢？是这个函数的原型吗？

> 上面例子中的解释：

* `Person`为构造函数
* `person1`、`person2`为`Person`的实例
* 构造函数的`prototype`属性指向，调用该构造函数而创建的实例的**原型**
* `Person.prototype`为`person1`的**原型**
* `person1`、`person2`继承了原型中的`name`属性


用一张图解释**构造函数**与**实例原型**的关系

![](https://s10.mogucdn.com/mlcdn/c45406/190421_21bijk293k7244lgcie0j4fgbe5g2_1058x578.png)

### __proto__

在上面的**prototype**中我们详细描述了**构造函数**如何与实例原型联系起来，那**实例**如何与**实例原型**之间如何联系呢？

在标准浏览器中构造函数的**实例**都拥有一个`__proto__`属性，通过这个**实例**上的**属性**可以找到这个实例的原型

![](https://s10.mogucdn.com/mlcdn/c45406/190421_1235011ggh2af3b01hj7941010l4l_990x668.png)

### constructor

每个原型都有一个 **constructor** 属性指向关联的构造函数

```
function Person() {

}
console.log(Person === Person.prototype.constructor); // true
```

![](https://s10.mogucdn.com/mlcdn/c45406/190421_1345h0c13a027556c48j45lj2ib2e_1104x556.png)

综上我们已经得出：

```
function Person() {

}

var person = new Person();

console.log(person.__proto__ == Person.prototype) // true
console.log(Person.prototype.constructor == Person) // true
// 顺便学习一个ES5的方法,可以获得对象的原型
console.log(Object.getPrototypeOf(person) === Person.prototype) // true
```

并且我们得出了：`构造函数`、`原型`、`实例`之间的关系

![](https://s10.mogucdn.com/mlcdn/c45406/190421_7b4h6c755ckcg3ig1719c71jjdlcc_1244x990.png)

## 实例与原型

当我们读取**对象**属性时，若我们读取的对象不存在，将会自动到对象的**原型**上查找属性是否存在，如果属性不存在将会到**原型的原型**上查找，一直会找到null为止

通过🌰我们来进行说明：

```
function Person() {

}

Person.prototype.name = 'Kevin';

var person = new Person();

person.name = 'Daisy';
console.log(person.name) // Daisy

delete person.name;
console.log(person.name) // Kevin
```

第一次log输出时我们得到了预期输出`Daisy`,随后我们通过`delete`关键词删除了person实例上的`name`属性，第二次输出是通过查询发现person实例中并不存在属性`name`，到`person`实例的原型`Person.prototype`上进行查找找到`name`属性，查询终止。

若`Person.prototype`上任然不存在`name`属性呢，将会从何处进行查询?

## 原型的原型

从`实例`与`实例原型`的关系里面可以知道，通过`__proto__`属性我们可以查询到期原型，那么原型的原型是什么呢?

通过这个🌰我们可以很清晰的知道，构造函数的原型的原型是`Object.prototype`,`Object.prototype`的原型是`null`

```
function Person(){}
Person.prototype.__proto__ === Object.prototype // true
Object.prototype.__proto__ === null // true
```

通过上述的知识点我们可以构建成一幅完整的关系：

![](https://s10.mogucdn.com/mlcdn/c45406/190421_7cebll7hhc7ea3jfe102f2g4fj4fa_836x772.png)

其中**青色**`__proto__`的线路就是我们通常所说的原型链


## 参考文章

* [you don't know js: this & prototype](https://github.com/getify/You-Dont-Know-JS/blob/1ed-zh-CN/this%20%26%20object%20prototypes/ch5.md)
* [JavaScript深入之从原型到原型链](https://github.com/mqyqingfeng/Blog/issues/2)


