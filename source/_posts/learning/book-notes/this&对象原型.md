---
title: this & 对象原型
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


### 基本字面量

在JavaScript中基本字面量会转换成对象



<p class="tip">一般来说，我们通过基本字面量：`let str = 'hello world';`创建的字符串，他只是个基本类型按道理来说不存在属性，但通过`str.length`却可以轻松渠道str字符串的长度，这是怎么回事呢，原来JavaScript会将**字面量形式的str**，转变成`String`对象形式的字符串</p>

> 基本字面量转变成对象的类型

* String
* Number
* Boolean
* RegExp




> 深浅拷贝

在进行深浅拷贝前，我们先明确，基本数据类型和复杂类型赋值的不同：

* 在我们进行赋值操作的时候，基本数据类型的赋值（=）是在内存中新开辟一段栈内存，然后再把再将值赋值到新的栈中
* 但是引用类型的赋值是传址。只是改变指针的指向，例如，也就是说引用类型的赋值是对象保存在栈中的地址的赋值，这样的话两个变量就指向同一个对象，因此两者之间操作互相有影响


> 赋值（=）和浅拷贝的区别

浅复制只会将对象的各个属性进行依次复制，并不会进行递归复制，而 JavaScript 存储对象都是存地址的，所以浅复制会导致赋值后的对象属性指向同一个内存地址


### 属性描述符


> 获取对象属性性质

```
var myObject = {
	a: 2
};

Object.getOwnPropertyDescriptor( myObject, "a" );
// {
//    value: 2,
//    writable: true,
//    enumerable: true,
//    configurable: true
// }
```


> 明确定义一个属性

```
var myObject = {};

Object.defineProperty( myObject, "a", {
	value: 2,
	writable: true,
	configurable: true,
	enumerable: true
} );

myObject.a; // 2
```

<p class="tip">使用 defineProperty(..)，我们手动、明确地在 myObject 上添加了一个直白的，普通的 a 属性。然而，你通常不会使用这种手动方法，除非你想要把描述符的某个性质修改为不同的值。</p>


> 修改属性性质

```
var myObject = {
    a: 2
};

Object.defineProperty( myObject, "a", {
	value: 2, 
	writable: true,
	configurable: true,
	enumerable: true 
} );

```

* value
    * 默认值：设置的初始值
* writable
    * 可修改性
    * 默认值：true
    * 将属性设置true后，修改属性值，将会发生`TypeError`(如果你试图改变一个不可配置属性的描述符定义，就会发生 TypeError)
* configurable
    * 可配置性
    * 能否通过defineProperty重新定义特性
    * 设置false后无法，更改特性
    * 默认值：true
    * 阻止的另外一个事情是使用 delete 操作符移除既存属性的能力
* enumerable
    * 可遍历性
    * 默认值：true


### 设置对象的几个方法

#### 防止扩展(Prevent Extensions)

`Object.preventExtensions(..)`


<p class="tip">不能添加新的属性</p>

```
var myObject = {
	a: 2
};

Object.preventExtensions( myObject );

myObject.b = 3;
myObject.b; // undefined
```

#### 封印（Seal）


`Object.Seal(..)`

<p class="tip">它实质上在当前的对象上调用 Object.preventExtensions(..)、并且属性标记为 configurable:false</p>

```
var myObject = {
	a: 2
};

Object.Seal( myObject );
```

#### 冻结（Freeze）

`Object.freeze(..)`

<p class="tip">Object.freeze(..) 创建一个冻结的对象，这意味着它实质上在当前的对象上调用 Object.seal(..)，同时也将它所有的“数据访问”属性设置为 writable:false，所以它们的值不可改变。</p>

### 混合（淆）“类”的对象


在JavaScript中是否存在一般语言类似于Java、C++类的概念，而JavaScript中的原型又是什么东西呢


<p class="tip">在JavaScript中类并不是我们想象中的类，JavaScript还是基于原型的概念进行设计，尽管它看起来存在：`new`、`instanceof`这些让你以为它是类的东西</p>

在开始了解前，我们先明白什么是类？

类是一种事物的抽象，拿建汽车来说，汽车需要：

* 轮胎
* 发动机
* 后视镜等等...

我们通过对汽车事物进行抽象，通过实例化产生新的汽车

并且类还包含继承、多态等概念：同样允许父类的泛化行为被子类覆盖，从而使它更加具体。实际上，相对多态允许我们在覆盖行为中引用基础行为

类的实例化上就是一个拷贝的过程，如下图：

![](https://s10.mogucdn.com/mlcdn/c45406/190408_13k6cb57lifabic37gi0889i67250_253x333.png)



> JavaScript中的"类"

<p class="tip">当你“继承”或是“实例化”时，JavaScript 的对象机制不会 自动地 执行拷贝行为。很简单，在 JavaScript 中没有“类”可以拿来实例化，只有对象。而且对象也不会被拷贝到另一个对象中，而是被 链接在一起</p>

在其他语言中观察到的类的行为意味着拷贝，让我们来看看 JS 开发者如何在 JavaScript 中 模拟 这种 缺失 的类的拷贝行为：mixins（混合）。我们会看到两种“mixin”：明确的（explicit） 和 隐含的（implicit）

## 三、原型（Prototype）


### Object.prototype

每个 普通 的 [[Prototype]] 链的最顶端，是内建的 Object.prototype。这个对象包含各种在整个 JS 中被使用的共通工具，因为 JavaScript 中所有普通（内建，而非被宿主环境扩展的）的对象都“衍生自”（也就是，使它们的 [[Prototype]] 顶端为）Object.prototype 对象。

你会在这里发现一些你可能很熟悉的工具，比如 .toString() 和 .valueOf()


### 设置与遮蔽属性

如果给一个对象添加属性，而这个属性或方法已经在其`[[Prototype]]`上已存在，这时是否会展现出"多态"特性，子属性

让我们来看下面的实例：

```
myObject.foo = "bar";
```

正如我们被暗示的那样，在 myObject 上的 foo 遮蔽没有看起来那么简单。我们现在来考察 myObject.foo = "bar" 赋值的三种场景，当 foo 不直接存在 于 myObject，但 存在 于 myObject 的 [[Prototype]] 链的更高层时：

* 如果一个普通的名为 foo 的数据访问属性在 [[Prototype]] 链的高层某处被找到，而且没有被标记为只读（writable:false），那么一个名为 foo 的新属性就直接添加到 myObject 上，形成一个 遮蔽属性。
* 如果一个 foo 在 [[Prototype]] 链的高层某处被找到，但是它被标记为 只读（writable:false） ，那么设置既存属性和在 myObject 上创建遮蔽属性都是 不允许 的。如果代码运行在 strict mode 下，一个错误会被抛出。否则，这个设置属性值的操作会被无声地忽略。不论怎样，没有发生遮蔽。
* 如果一个 foo 在 [[Prototype]] 链的高层某处被找到。没有 foo 会被添加到（也就是遮蔽在）myObject 上。**必须使用 Object.defineProperty(..)**


### “类”

现在你可能会想知道：“为什么 一个对象需要链到另一个对象？” 真正的好处是什么？这是一个很恰当的问题，但在我们能够完全理解和体味它是什么和如何有用之前，我们必须首先理解 [[Prototype]] 不是 什么。

在 JavaScript 中，对于对象来说没有抽象模式/蓝图，即没有面向类的语言中那样的称为类的东西。JavaScript 只有 对象。

实际上，在所有语言中，JavaScript 几乎是独一无二的，也许是唯一的可以被称为“面向对象”的语言，因为可以根本没有类而直接创建对象的语言很少，而 JavaScript 就是其中之一。

在 JavaScript 中，类不能（因为根本不存在）描述对象可以做什么。对象直接定义它自己的行为。这里 仅有 对象。


### “类”函数


```
function Foo() {
	// ...
}

var a = new Foo();

Object.getPrototypeOf( a ) === Foo.prototype; // true
```

在面向类的语言中，可以制造一个类的多个 拷贝（即“实例”），就像从模具中冲压出某些东西一样。我们在第四章中看到，这是因为初始化（或者继承）类的处理意味着，“将行为计划从这个类拷贝到物理对象中”，对于每个新实例这都会发生。

但是在 JavaScript 中，没有这样的拷贝处理发生。你不会创建类的多个实例。你可以创建多个对象，它们的 [[Prototype]] 连接至一个共通对象。但默认地，没有拷贝发生，如此这些对象彼此间最终不会完全分离和切断关系，而是 链接在一起。



### 总结

当试图在一个对象上进行属性访问，而对象又没有该属性时，对象内部的 [[Prototype]] 链接定义了 [[Get]] 操作（见第三章）下一步应当到哪里寻找它。这种对象到对象的串行链接定义了对象的“原形链”（和嵌套的作用域链有些相似），在解析属性时发挥作用。

所有普通的对象用内建的 Object.prototype 作为原形链的顶端（就像作用域查询的顶端是全局作用域），如果属性没能在链条的前面任何地方找到，属性解析就会在这里停止。toString()，valueOf()，和其他几种共同工具都存在于这个 Object.prototype 对象上，这解释了语言中所有的对象是如何能够访问他们的。

在 JavaScript 中的关键区别是，没有拷贝发生。取而代之的是对象最终通过 [[Prototype]] 链链接在一起。

<p class="tip">当一个属性/方法引用在一个对象上发生，而这样的属性/方法又不存在时，这个链接就会被使用。在这种情况下，[[Prototype]] 链接告诉引擎去那个被链接的对象上寻找该属性/方法。接下来，如果那个对象也不能满足查询，就沿着它的 [[Prototype]] 查询，如此继续。这种对象间的一系列链接构成了所谓的“原形链”。
</p>


