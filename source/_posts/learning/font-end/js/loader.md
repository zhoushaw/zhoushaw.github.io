---
title: loader入门
date: 2019-07-29 4:17:35
categories: js
tags: js
---


## 前言

Loader 就像是一个翻译员，能把源文件经过转化后输出新的结果，并且一个文件还可以链式的经过多个翻译员翻译。

可以通过loader对源码进行解析编译，生成新的代码，例如babel-loader，就是对源码进行编译解析将es6转换成es5代码

> Loader 基础

由于 Webpack 是运行在 Node.js 之上的，一个 Loader 其实就是一个 Node.js 模块，这个模块需要导出一个函数。 这个导出的函数的工作就是获得处理前的原内容，对原内容执行处理后，返回处理后的内容。

```
module.exports = function(source) {
  // source 为 compiler 传递给 Loader 的一个文件的原内容
  // 该函数需要返回处理后的内容，这里简单起见，直接把原内容返回了，相当于该 Loader 没有做任何转换
  return source;
};
```

## 关于学习AST转换的一些文档

* [babel-handbook](https://github.com/jamiebuilds/babel-handbook/blob/master/translations/en/user-handbook.md)
* [babel-types](https://babeljs.io/docs/en/babel-types#functionexpression)
* [ast-explorer](https://astexplorer.net/)



## Babel 的处理步骤

Babel 的三个主要处理步骤分别是：
 
* `解析（parse）`
* `转换（transform）`
* `生成（generate）`

> 解析

解析步骤接收代码并输出 AST。 这个步骤分为两个阶段：**词法分析（Lexical Analysis） **和 语法分析（Syntactic Analysis）。

> 转换

转换步骤接收 AST 并对其进行遍历，在此过程中对节点进行添加、更新及移除等操作

> 生成

代码生成步骤把最终（经过一系列转换之后）的 AST 转换成字符串形式的代码，同时还会创建源码映射（source maps）

### 解析

在进行代码转换前，需要将代码转换成AST语法，可以通过`babel`提供的`parser`工具进行转换，具体转换成ast代码如下：


```
// 安装依赖 npm install @babel/parser
const parser = require("@babel/parser");
// 其中code为提供的源码
let code = `
    function testFn() {
    
    }
`;
const ast = parser.parse(code);
```

## 转换

> 遍历

要进行代码转换必须对AST进行遍历，它遍历的顺序是按照**树的深度遍历**进行

![](https://s10.mogucdn.com/mlcdn/c45406/190821_1736cgd1g5khfa8a4dfj11k7cebf7_440x376.png)

详细遍历过程可参考：[traverse遍历规则](https://github.com/jamiebuilds/babel-handbook/blob/master/translations/zh-Hans/plugin-handbook.md#%E9%81%8D%E5%8E%86)

> 如何通过babel访问并修改ast节点

我们可以通过`@babel/parser`npm包对ast进行访问，具体实现代码如下:

## 从零开发一个loader

###利用 loader-runner 调试 Loaders


[loader-runner](https://www.npmjs.com/package/loader-runner) 允许你不依靠 webpack 单独运行 loader


```
mkdir loader-example && cd $_
touch index.js  // 创建需要转换的数据源
npm init
npm install loader-runner --save-dev
```

> 创建运行loader文件

* step1

```
touch run-loader.js
```

* step2

```
//run-loader.js
const fs = require("fs");
const path = require("path");
const { runLoaders } = require("loader-runner");

runLoaders(
  {
    resource: "./index.js", // 转换源
    loaders: [path.resolve(__dirname, "./loader-demo.js")], // loader地址
    readResource: fs.readFile.bind(fs),
  },
  // 第二个参数，是一个函数形参是错误、转换结果
  (err, result) => {
    if (err) {
        console.error(err)
        return;
    } 
    //输出转换结果到output.js中
    fs.writeFileSync("./output.js", result.result)
  }
);
```

> 创建loader

* step1

```
touch loader-demo.js
```

* step2

```
module.exports = function(source) {
  // ... 对source进行转换
  return source;
};
```

## 通过AST对代码进行改造

`抽象语法树是源代码语法结构的一种抽象表示。它以树状的形式表现编程语言的语法结构，树上的每个节点都表示源代码中的一种结构`

> 功能

通过 AST 可以实现很多非常有用的功能，例如将 ES6 以后的代码转为 ES5，eslint 的检查，代码美化，甚至 js 引擎都是依赖 AST 实现的，同时因为代码本质只是单纯的字符串，所以并不仅限于 js 之间的转换，scss，less 等 css 预处理器也是通过 AST 转为浏览器认识的 css 代码


> 起步

* step1

`npm install @babel/parser @babel/traverse @babel/types @babel/core --save-dev`



