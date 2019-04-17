---
title: types & grammar
date: 2019-4-1 4:36:35
categories: js
tags: js
---

## 一、类型


> 基本类型

JavaScript 定义了七种内建类型：

null
undefined
boolean
number
string
symbol -- 在 ES6 中被加入的！
object

**注意**： 除了 object 所有这些类型都被称为“基本类型（primitives）”。


> 类型检测

typeof 操作符可以检测给定值的类型，而且总是返回七种字符串值中的一种

```
typeof undefined     === "undefined"; // true
typeof true          === "boolean";   // true
typeof 42            === "number";    // true
typeof "42"          === "string";    // true
typeof { life: 42 }  === "object";    // true

// 在 ES6 中被加入的！
typeof Symbol()      === "symbol";    // true
```

在上面的列表中剔除了 null。它是 特殊的 -- 特殊在它与 typeof 操作符组合时是有 bug 的。

```
typeof null === "object"; // true
```

### undefined vs "undeclared"

当前 还不拥有值的变量，实际上拥有 undefined 值。对这样的变量调用 typeof 将会返回 `"undefined"`：

```
var a;

typeof a; // "undefined"

var b = 42;
var c;

// 稍后
b = c;

typeof b; // "undefined"
typeof c; // "undefined"
```

大多数开发者考虑“undefined”这个词的方式会诱使他们认为它是“undeclared（未声明）”的同义词。然而在 JS 中，这两个概念十分不同。

一个“undefined”变量是在可访问的作用域中已经被声明过的，但是在 这个时刻 它里面没有任何值。相比之下，一个“undeclared”变量是在可访问的作用域中还没有被正式声明的。

> 考虑这段代码：

```
var a;

a; // undefined
b; // ReferenceError: b is not defined
```

在上面代码中，b未声明时进行了使用，浏览器反馈的错误是：`b is not defined`.这当然很容易而且很合理地使人将它与“b is undefined.”搞混。需要重申的是，“undefined”和“is not defined”是非常不同的东西。要是浏览器能告诉我们类似于“b is not found”或者“b is not declared”之类的东西就好了，那会减少这种困惑！


```
var a;

typeof a; // "undefined"

typeof b; // "undefined"
```

`type` 对于未undeclared的变量，返回值也是`undefined`。即使 是一个未声明变量，也不会有错误被抛出。这是 typeof 的一种特殊的安全防卫行为


### typeof Undeclared

由于typeof安全防卫的特性，我们可以将其用来判断一个变量是否在作用域内进行了赋值操作，倘若不使用typeof，若变量不存在将会发生异常

```
if (typeof sss === "undefined") {
	sss = function() { /*..*/ };
}
``

> 使用场景


作为一个简单的例子，想象在你的程序中有一个“调试模式”，它是通过一个称为 DEBUG 的全局变量（标志）来控制的。在实施类似于在控制台上输出一条日志消息这样的调试任务之前，你想要检查这个变量是否被声明了。一个顶层的全局 var DEBUG = true 声明只包含在一个“debug.js”文件中，这个文件仅在你开发/测试时才被加载到浏览器中，而在生产环境中则不会。

然而，在你其他的程序代码中，你不得不小心你是如何检查这个全局的 DEBUG 变量的，这样你才不会抛出一个 ReferenceError。这种情况下 typeof 上的安全防卫就是我们的朋友。

```
// 噢，这将抛出一个错误！
if (DEBUG) {
	console.log( "Debugging is starting" );
}

// 这是一个安全的存在性检查
if (typeof DEBUG !== "undefined") {
	console.log( "Debugging is starting" );
}
```


