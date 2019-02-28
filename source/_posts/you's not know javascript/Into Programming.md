---
title: 译文：you don't know js 之 Into Programming
date: 2019-02-28 8:20:15
tags: book
categories: js
---



## Chapter 1: Into Programming

Welcome to the You Don't Know JS (YDKJS) series.

欢迎来到你不懂js系列

<div><!-- more--></div>

Up & Going is an introduction to several basic concepts of programming -- of course we lean toward JavaScript (often abbreviated JS) specifically -- and how to approach and understand the rest of the titles in this series. Especially if you're just getting into programming and/or JavaScript, this book will briefly explore what you need to get up and going.

Up & Going是为了介绍程序基本概念的，当然我们特别倾向于javascript(通常简称为JS)，如何看待与裂解本系列其他书目。如果你准备好进入程序或者javascript了。这本书将简单浏览你需要什么来入门与进阶。

This book starts off explaining the basic principles of programming at a very high level. It's mostly intended if you are starting YDKJS with little to no prior programming experience, and are looking to these books to help get you started along a path to understanding programming through the lens of JavaScript.

本书开始解释程序的基础原则在很高的级别。如果你开始阅读YDKJS带有较少或没有程序经验并且寻找这些书通过javascrpt去帮助你开始理解程序，那么本书的主要目的就是帮助你了解如何开始YDKJS。

Chapter 1 should be approached as a quick overview of the things you'll want to learn more about and practice to get into programming. There are also many other fantastic programming introduction resources that can help you dig into these topics further, and I encourage you to learn from them in addition to this chapter.

第一章应该适合快速的预览你想要学习和训练进入程序。这里有很多能帮助你深入这些话题的有用的程序资源，我鼓励你在这一章之外向他们学习。

Once you feel comfortable with general programming basics, Chapter 2 will help guide you to a familiarity with JavaScript's flavor of programming. Chapter 2 introduces what JavaScript is about, but again, it's not a comprehensive guide -- that's what the rest of the YDKJS books are for!

一旦你对普通的程序基础适应了，第二章将会帮助你熟悉javascript的程序。第二章介绍了javascript是关于什么的，再者，它不只是全面的指南 -- 这是其余YDKJS系列书的作用。

If you're already fairly comfortable with JavaScript, first check out Chapter 3 as a brief glimpse of what to expect from YDKJS, then jump right in!

如果你已经很熟练javascript，那么首先快速的预览一下第三章，然后快速的进入学习吧。

##Code

Let's start from the beginning.

让我们从这开始吧。

A program, often referred to as source code or just code, is a set of special instructions to tell the computer what tasks to perform. Usually code is saved in a text file, although with JavaScript you can also type code directly into a developer console in a browser, which we'll cover shortly.

一个程序，经常被交付源码或者就是编码，去设置了一个特殊的介绍告诉计算机哪些任务被执行。通常代码被使用文本文件存储，通过javascript，你也可以输入代码直接在浏览器的开发者区输入代码，稍后我们会讲到这一点。

The rules for valid format and combinations of instructions is called a computer language, sometimes referred to as its syntax, much the same as English tells you how to spell words and how to create valid sentences using words and punctuation.

Statements
In a computer language, a group of words, numbers, and operators that performs a specific task is a statement. In JavaScript, a statement might look as follows:


```
a = b * 2;
```

The characters a and b are called variables (see "Variables"), which are like simple boxes you can store any of your stuff in. In programs, variables hold values (like the number 42) to be used by the program. Think of them as symbolic placeholders for the values themselves.

By contrast, the 2 is just a value itself, called a literal value, because it stands alone without being stored in a variable.

The = and * characters are operators (see "Operators") -- they perform actions with the values and variables such as assignment and mathematic multiplication.

Most statements in JavaScript conclude with a semicolon (;) at the end.

The statement a = b * 2; tells the computer, roughly, to get the current value stored in the variable b, multiply that value by 2, then store the result back into another variable we call a.

Programs are just collections of many such statements, which together describe all the steps that it takes to perform your program's purpose.

Expressions
Statements are made up of one or more expressions. An expression is any reference to a variable or value, or a set of variable(s) and value(s) combined with operators.

For example:


```
a = b * 2;
```
This statement has four expressions in it:

2 is a literal value expression
b is a variable expression, which means to retrieve its current value
b * 2 is an arithmetic expression, which means to do the multiplication
a = b * 2 is an assignment expression, which means to assign the result of the b * 2 expression to the variable a (more on assignments later)
A general expression that stands alone is also called an expression statement, such as the following:

b * 2;
This flavor of expression statement is not very common or useful, as generally it wouldn't have any effect on the running of the program -- it would retrieve the value of b and multiply it by 2, but then wouldn't do anything with that result.

A more common expression statement is a call expression statement (see "Functions"), as the entire statement is the function call expression itself:

```
alert( a );
```

