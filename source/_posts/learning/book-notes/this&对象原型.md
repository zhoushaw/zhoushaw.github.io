---
title: this&对象原型
date: 2019-4-1 4:36:35
categories: js
tags: js
---

## 一、this关键词


<p class="tip">this是关键词，表示指向的索引位置</p>

很多人对于this最终指向常见的误解是，this是编写时绑定的，通常会将其认为成一下几种情况：


1、认为this指向，foo函数

```javascript
function foo () {
    console.log(this);
}
foo();
```

<div><!--more--></div>

2、认为this指向，obj对象

```javascript
function foo() {
	console.log( this.a );
}

var obj = {
	a: 2,
	foo: foo
};

var bar = obj.foo; // 函数引用！

var a = "oops, global"; // `a` 也是一个全局对象的属性

bar(); // "oops, global"
```

### 可以大致分为以下几种情况：

函数调用方式与内部this指针关系
1.直接调用:函数内部this指向全局对象window
2.通过对象使用点来调用:函数内部this指向调用对象
3.触发事件调用函数:函数内部的this指向触发事件的对象
4.以new的方式来调用:函数内部this指向本次函数执行时对应的一个匿名对象（以new的方式创建的函数，函数名的首字母一般以大写字母开始）
构造函数 ，是一种特殊的方法。主要用来在创建对象时初始化对象， 即为对象成员变量赋初始值，总与new运算符一起使用在创建对象的语句中。

5.通过call的方法来间接调用方法:函数内部this指向call方法的第一参数对象
有点:我们可以创建结构相同，但内容不同的对象


按照本文中的分类将其分为四大块：

默认绑定、隐含绑定、明确绑定、new 绑定




### 仅仅是规则

this的最终指向可以将其分为大致四种规则

#### 默认绑定

我们要考察的第一种规则源于函数调用的最常见的情况：独立函数调用

在非`strict mode`模式下，独立函数调用默认指向全局对象window，在`strict mode`模式下默认绑定 来说全局对象是不合法，所以 `this` 将被设置为 `undefined`

```
function foo() {
	console.log( this.a );
}

var a = 2;

foo(); // 2
```

#### 隐含绑定

另一种要考虑的规则是：调用点是否有一个环境对象（`context object`），也称为拥有者（`owning`）或容器（`containing`）对象


```
function foo() {
	console.log( this.a );
}

var obj = {
	a: 2,
	foo: foo
};

obj.foo(); // 2
```

<p class="tip">无论 foo() 是否一开始就在 obj 上被声明，还是后来作为引用添加（如上面代码所示），这个 函数 都不被 obj 所真正“拥有”或“包含”.调用点 使用 obj 环境来 引用 函数，所以你 可以说 obj 对象在函数被调用的时间点上“拥有”或“包含”这个 函数引用。</p>


只有对象属性引用链的最后一层是影响调用点的。比如：

```
function foo() {
	console.log( this.a );
}

var obj2 = {
	a: 42,
	foo: foo
};

var obj1 = {
	a: 2,
	obj2: obj2
};

obj1.obj2.foo(); // 42
```

##### 隐含丢失


传递一个回调函数时：

```
function foo() {
	console.log( this.a );
}

function doFoo(fn) {
	// `fn` 只不过 `foo` 的另一个引用

	fn(); // <-- 调用点!
}

var obj = {
	a: 2,
	foo: foo
};

var a = "oops, global"; // `a` 也是一个全局对象的属性

doFoo( obj.foo ); // "oops, global"
```

那么如果接收你所传递回调的函数不是你的，而是语言内建的呢？没有区别，同样的结果。

```
function foo() {
	console.log( this.a );
}

var obj = {
	a: 2,
	foo: foo
};

var a = "oops, global"; // `a` 也是一个全局对象的属性

setTimeout( obj.foo, 100 ); // "oops, global"
```

正如我们刚刚看到的，我们的回调函数丢掉他们的 this 绑定是十分常见的事情。但是 this 使我们吃惊的另一种方式是，接收我们回调的函数故意改变调用的 this。那些很流行的 JavaScript 库中的事件处理器就十分喜欢强制你的回调的 this 指向触发事件的 DOM 元素。虽然有时这很有用，但其他时候这简直能气死人。不幸的是，这些工具很少给你选择。

#### 明确绑定

JavaScript 语言中的“所有”函数都有一些工具。具体地说，函数拥有 call(..) 和 apply(..) 方法。

这些工具如何工作？它们接收的第一个参数都是一个用于 this 的对象，之后使用这个指定的 this 来调用函数。因为你已经直接指明你想让 this 是什么，所以我们称这种方式为 明确绑定（explicit binding)。

```
function foo() {
	console.log( this.a );
}

var obj = {
	a: 2
};

foo.call( obj ); // 2
```



##### API 调用的“环境”

```
function foo(el) {
	console.log( el, this.id );
}

var obj = {
	id: "awesome"
};

// 使用 `obj` 作为 `this` 来调用 `foo(..)`
[1, 2, 3].forEach( foo, obj ); // 1 awesome  2 awesome  3 awesome
```


#### new 绑定

当使用 new 操作符来初始化一个类时，这个类的构造器就会被调用。通常看起来像这样：

```
something = new MyClass(..);
```

<p class="tip">实际上 JavaScript 的机制和 new 在 JS 中的用法所暗示的面向类的功能 没有任何联系。在 JS 中，构造器 仅仅是一个函数，它们偶然地与前置的 new 操作符一起调用。它们不依附于类，它们也不初始化一个类。它们甚至不是一种特殊的函数类型。它们本质上只是一般的函数，在被使用 new 来调用时改变了行为。</p>

> 当在函数前面被加入 new 调用时，也就是构造器调用时，下面这些事情会自动完成：

* 一个全新的对象会凭空创建（就是被构建）
* 这个新构建的对象会被接入原形链（[[Prototype]]-linked）
* 这个新构建的对象被设置为函数调用的 this 绑定
* 除非函数返回一个它自己的其他 对象，否则这个被 new 调用的函数将 自动 返回这个新构建的对象。


简单来说通过new方法初始化的构造器this指向函数本身

```
function foo(a) {
	this.a = a;
}

var bar = new foo( 2 );
console.log( bar.a ); // 2
```


### 一切皆有顺序



<p class="tip">上面已经揭示了四种this绑定最终指向的规则，但是指向的规则可能会出现重叠的情况，当两种以上的规则出现后如何抉择优先顺序呢。</p>

* 函数是通过 new 被调用的吗（new 绑定）？如果是，this 就是新构建的对象。
   * var bar = new foo()
* 函数是通过 call 或 apply 被调用（明确绑定），甚至是隐藏在 bind 硬绑定 之中吗？如果是，this 就是那个被明确指定的对象。
    * var bar = foo.call( obj2 )
* 函数是通过环境对象（也称为拥有者或容器对象）被调用的吗（隐含绑定）？如果是，this 就是那个环境对象。
    * var bar = obj1.foo()
* 否则，使用默认的 this（默认绑定）。如果在 strict mode 下，就是 undefined，否则是 global 对象。
    * var bar = foo()


### 绑定的特例

正如通常的那样，对于“规则”总有一些 例外。

#### 被忽略的 this

<p class="tip">如果你传递 null 或 undefined 作为 call、apply 或 bind 的 this 绑定参数，那么这些值会被忽略掉，取而代之的是 默认绑定 规则将适用于这个调用。</p>

```
function foo() {
	console.log( this.a );
}

var a = 2;

foo.call( null ); // 2
```

> 更安全的 this

```
function foo(a,b) {
	console.log( "a:" + a + ", b:" + b );
}

// 我们的 DMZ 空对象
var ø = Object.create( null );

// 将数组散开作为参数
foo.apply( ø, [2, 3] ); // a:2, b:3

// 用 `bind(..)` 进行 currying
var bar = foo.bind( ø, 2 );
bar( 3 ); // a:2, b:3
```

可以通过让其指向一个空对象，使其按照`硬绑定`原则进行

#### 间接

通过赋值

```
function foo() {
	console.log( this.a );
}

var a = 2;
var o = { a: 3, foo: foo };
var p = { a: 4 };

o.foo(); // 3
(p.foo = o.foo)(); // 2
```


### 词法this


> 一个箭头函数的词法绑定是不能被覆盖

```
function foo() {
  // 返回一个箭头函数
	return (a) => {
    // 这里的 `this` 是词法上从 `foo()` 采用的
		console.log( this.a );
	};
}

var obj1 = {
	a: 2
};

var obj2 = {
	a: 3
};

var bar = foo.call( obj1 );
bar.call( obj2 ); // 2, 不是3!
```

> 它们本质是使用广为人知的词法作用域来禁止了传统的 `this` 机制

```
function foo() {
	var self = this; // 词法上捕获 `this`
	setTimeout( function(){
		console.log( self.a );
	}, 100 );
}

var obj = {
	a: 2
};

foo.call( obj ); // 2
```

## 二、对象

前面我们讲解了 this 绑定如何根据函数调用的调用点指向不同的对象。但究竟什么是对象，为什么我们需要指向它们？

### 语法


<p class="tip">对象来自于两种形式：声明（字面）形式，和构造形式。</p>


> 一个对象的字面语法看起来像这样：

```
var myObj = {
	key: value
	// ...
};
```

> 构造形式看起来像这样：

```
var myObj = new Object();
myObj.key = value;
```

构造形式和字面形式的结果是完全同种类的对象。唯一真正的区别在于你可以向字面声明一次性添加一个或多个键/值对，而对于构造形式，你必须一个一个地添加属性。


### 类型

> JS 的六种主要类型

* string
* number
* boolean
* null
* undefined
* object


> 内建对象

* String
* Number
* Boolean
* Object
* Function
* Array
* Date
* RegExp
* Error


