title: Event loop
date: 2019-3-1 4:36:35
categories: js
tags: js
---

## 前言

> 请问下面输出的结果是什么

```
console.log('script start');

setTimeout(function() {
  console.log('setTimeout');
}, 0);

Promise.resolve().then(function() {
  console.log('promise1');
}).then(function() {
  console.log('promise2');
});

console.log('script end');
```

纳尼？？仿佛又回想了当初被面试官支配时的恐惧了！！

骚年稳住别慌，这道面试题考察的是你对Event loop事件循环的理解，当你深入了解浏览器或Node中如何处理事件循环的时候，上面此类题目对你来说就是so easy，好了话不多说让我们快速进入正题吧。

<div><!--more--></div>


## Event loop

> 是什么

**Event loop**即事件循环，是浏览器和Node环境中运行**单线程JavaScript**一种不阻塞运行的一种机制。也就是我们常常称之为的异步的原理。

> 有什么作用

* 类似于上面问答中的代码，一般情况下是不会产生的。但是由于一些业务场景迫使我们**不可避免的编写出多个异步事件**，而我们对其**运行顺序不知其所以然**，难免会造成不必要的困扰

* 当然Event loop也是面试场上的常胜将军，大多数同学都**折戟于此**

* 市场上框架、新技术层出不穷，想要在风云突变的战场上稳住脚跟就必须**修炼好内功**，了解一些底层原理无非是非常好的路径


## 储备知识

在正式Event loop讲解前，我们先回顾一下基本数据结构知识

> 队列

队列是一种操作受限制的线性表，它只运行从**表的前端(front)**进行删除操作，**表的后端(rear)**进行添加操作。

进行删除操作的称之为**表头**，添加操作的称之为**表尾**，空的队列称之为**空队列**。

队列的线性结构赋予**其先进先出**的特性

![](https://s10.mogucdn.com/mlcdn/c45406/190301_80cgh13fd23fjkahjd296l7ig9e68_1152x241.jpg)

> 栈

栈是一种操作受限制的线性表，它只运行从表的**尾端(rear)**进行**添加操作和删除操作**

栈的限制结构赋予其**先进后出**的特性

![](https://s10.mogucdn.com/mlcdn/c45406/190301_3g51f9k9h099ga3lecj98d6adchh5_1344x752.jpg)


## Event loop任务

在JavaScript中，会将执行的任务分为两类，一种是**宏任务**(MacroTask)简称为**Task**,另一种是**微任务**(MicroTask)

> 宏任务类型

**script全部代码**、**setTimeout**、**setInterval**、**I/O**、**UI Rendering**


> 微任务

**Process.nextTick**（Node独有）、**Promise**、**MutationObserver**


## 浏览器Event loop

在JavaScript中有一个**主线程**(main thread) 和**调用栈** (call-stack) ,所有任务都会被放到调用栈等待主线程执行。

> JS调用栈

JS调用栈采用栈结构，是先进后出规则，当函数执行的时候会放到栈的顶部，当函数执行完成会将函数从栈顶移除，遇到新函数会新函数将推入栈内，执行完成从栈顶移除，直到栈被清空

列如:

```
function task1 () {
    console.log('task1');
}
function task2 () {
    task1();
    console.log('hello world');
}
task2();
```


执行到task1()时，栈内容为:task2 task1，依次执行并移除task1、task2


> 同步任务和异步任务

在JavaScript将任务分为同步任务和异步任务，同步任务将依次放入调用栈中按照先进后出的规则，放入主线程执行。异步任务则是等待执行结果返回后放入任务队列中等待主线程空闲时(调用栈为空时，同步任务被执行完成时)，被读取到调用栈内等待主线程执行。


简单来说可以将其区域分为三个区域:

* 任务队列区
* 主线程执行区
* MacroTask区
* MicroTask区

> 任务之间执行顺序

JavaScript代码在运行时，主线程顺序执行代码，按照栈的结构先进后出，将微任务存入微任务区，宏任务存入宏任务区。
## 
当任务队列任务为空时，将会查看MicroTask区队列是否为空，若为空则查询MacroTask区并执行。若不为空则执行MicroTask区任务，若遇到任务中存在MacroTask将存入MacroTask区队尾。执行MicroTask任务完成后将，执行MacroTask区任务


## 解答文章头部提出的问题

```
console.log('script start');

setTimeout(function() {
  console.log('setTimeout');
}, 0);

Promise.resolve().then(function() {
  console.log('promise1');
}).then(function() {
  console.log('promise2');
});

console.log('script end');
```

JavaScript在运行这段代码逐行执行，按照调用栈、宏任务、微任务执行过程如下:

```
#过程一:

MicroTask: 
MacroTask: setTimeout

call-Task: 

Log: script start


#过程二:

MicroTask: Promise.then
MacroTask: setTimeout

call-Task: 

Log: script start

#过程三:

MicroTask: 
MacroTask: setTimeout

call-Task: Promise.then

Log:  script start、 script end

#过程四:

MicroTask: Promise.then promise2
MacroTask: setTimeout

call-Task: 

Log:  script start、 script end、promise1

#过程五:

MicroTask: 
MacroTask: setTimeout

call-Task: Promise.then promise2

Log:  script start、 script end、promise1

#过程五:

MicroTask: 
MacroTask: setTimeout

call-Task: 

Log:  script start、 script end、promise1、promise2

#过程六:

MicroTask: 
MacroTask:

call-Task: setTimeout

Log:  script start、 script end、promise1、promise2

#过程七:

MicroTask: 
MacroTask:

call-Task:

Log:  script start、 script end、promise1、promise2、setTimeout
```





