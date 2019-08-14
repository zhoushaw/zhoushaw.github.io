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



