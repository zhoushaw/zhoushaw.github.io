title: typescript
date: 2018-6-9 4:36:35
categories: js
tags:   js
---


<div><!--more--></div>

## 起步

> compile

`sudo npm install typescript -g`

> vscode环境配置

1.项目目录下新建tsconfig.json文件

```
{
    "compilerOptions": {

        "module": "commonjs",
        "target": "es5",
        "noImplicitAny": false,
        "sourceMap": false,
        "outDir": "src"
    }
}
```
 2.使用快捷键 command ＋ shift + b

* 选择tsc构建: 创建typescript构建环境
* 选择tsc监视: 监视typescript

## 数据类型

> javascript原始类型

* string
* undefined
* number
* boolean
* null
* object
* symbol

> ts数据类型表示

1.布尔
`let isDone: boolean = false;`
2.数值
`let decLiteral: number = 6;`
3.字符串
`let myName: string = 'Tom';`
4.空值
`let unusable: void = undefined;`
5.任意
`let myFavoriteNumber: any = 'seven';`
6.undefined和null
`let num: number = undefined;`
`let n: null = null;`
**undefined和null类型的值可以赋给其他类型的值**
7.void
`let u: void;`
**不可以赋值给其他类型**

8.联合类型
`let myFavoriteNumber: string | number;`

> 注意

**在typescript中没有定义类型将会自动为其匹配对应的类型**

## 概念

> 对象的类型——接口

**在面向对象语言中，接口（Interfaces）是一个很重要的概念，它是对行为的抽象，而具体如何行动需要由类（classes）去实现（implements）。**

```
interface Person {
    name: string;
    age: number;
}

let tom: Person = {
    name: 'Tom',
    age: 25
};
```

**可选属性**

```
interface Person {
    name: string;
    age?: number;
}

let tom: Person = {
    name: 'Tom'
};
```

**任意属性**

```
interface Person {
    name: string;
    age?: number;
    [propName: string]: any;
}

let tom: Person = {
    name: 'Tom',
    gender: 'male'
};
```

**只读**

```
interface Person {
    readonly id: number;
    name: string;
    age?: number;
    [propName: string]: any;
}

let tom: Person = {
    name: 'Tom',
    gender: 'male'
};

tom.id = 89757;
```

> 数组类型

**「类型 + 方括号」表示法**
`let fibonacci: number[] = [1, 1, 2, 3, 5];`

**任意类型**
`let list: any[] = ['Xcat Liu', 25, { website: 'http://xcatliu.com' }];`

**类数组**

```
function sum() {
    let args: IArguments = arguments;
}
```


> 函数类型

**一个函数有输入和输出，要在 TypeScript 中对其进行约束，需要把输入和输出都考虑到**

```
function sum(x: number, y: number): number {
    return x + y;
}
```

**函数表达式**

```
let mySum = function (x: number, y: number): number {
    return x + y;
};
```
**在 TypeScript 的类型定义中，=> 用来表示函数的定义，左边是输入类型，需要用括号括起来，右边是输出类型。**

```
let mySum: (x: number, y: number) => number = function (x: number, y: number): number {
    return x + y;
};
```

**接口定义函数形状**


```
interface SearchFunc {
    (source: string, subString: string): boolean;
}

let mySearch: SearchFunc;
mySearch = function(source: string, subString: string) {
    return source.search(subString) !== -1;
}
```

**可选参数**

```
function buildName(firstName: string, lastName?: string) {
    if (lastName) {
        return firstName + ' ' + lastName;
    } else {
        return firstName;
    }
}
let tomcat = buildName('Tom', 'Cat');
let tom = buildName('Tom');
```
**可选参数后面不允许再出现必须参数了**

**默认参数**

```
function buildName(firstName: string, lastName: string = 'Cat') {
    return firstName + ' ' + lastName;
}
let tomcat = buildName('Tom', 'Cat');
let tom = buildName('Tom');
```

**重载**

重载允许一个函数接受不同数量或类型的参数时，作出不同的处理

```
function reverse(x: number | string): number | string {
    if (typeof x === 'number') {
        return Number(x.toString().split('').reverse().join(''));
    } else if (typeof x === 'string') {
        return x.split('').reverse().join('');
    }
}
```


##类型断言
**类型断言（Type Assertion）可以用来手动指定一个值的类型。**
语法:
<类型>值       或       值 as 类型

> 为何需要类型断言

**当 TypeScript 不确定一个联合类型的变量到底是哪个类型的时候，我们只能访问此联合类型的所有类型里共有的属性或方法**
number类型中没有length属性，会报错

```
function getLength(something: string | number): number {
    return something.length;
}
```

这时可以将变量断言成某种类型

```
function getLength(something: string | number): number {
    if ((<string>something).length) {
        return (<string>something).length;
    } else {
        return something.toString().length;
    }
}
```

## 声明文件

**假如我们想使用第三方库，比如 jQuery，我们通常这样获取一个 id 是 foo 的元素，但是在 TypeScript 中，我们并不知道 $ 或 jQuery 是什么东西**

```
declare var jQuery: (string) => any;
jQuery('#foo');
```
> 声明文件

**通常我们会把类型声明放到一个单独的文件中，这就是声明文件**

```
// jQuery.d.ts
declare var jQuery: (string) => any;
```

引入申明文件

```
/// <reference path="./jQuery.d.ts" />
jQuery('#foo');
```

> 申明方法

[npm](https://blogs.msdn.microsoft.com/typescript/2016/06/15/the-future-of-declaration-files/)


## 内置对象

> ECMAScript 标准提供的内置对象

**Boolean**、**Error**、**Date**、**RegExp** 等。

定义方式:

```
let b: Boolean = new Boolean(1);
let e: Error = new Error('Error occurred');
let d: Date = new Date();
let r: RegExp = /[a-z]/;
```

> DOM 和 BOM 的内置对象

```
let body: HTMLElement = document.body;
let allDiv: NodeList = document.querySelectorAll('div');
document.addEventListener('click', function(e: MouseEvent) {
  // Do something
});
```

## 类型别名


```
type Name = string;
type NameResolver = () => string;
type NameOrResolver = Name | NameResolver;
function getName(n: NameOrResolver): Name {
    if (typeof n === 'string') {
        return n;
    }
    else {
        return n();
    }
}

```


