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

有效的格式和混合的指令被称之为计算机语言，有时被作为它的预发，更像是英语告诉你如何使用单词和标点拼写单词并且如何创造有效的句子。

##Statements

In a computer language, a group of words, numbers, and operators that performs a specific task is a statement. In JavaScript, a statement might look as follows:

在计算机中，一组单词、数字和运算符执行一个特殊的任务是一个句子。在javascript中一个句子可能看来像下面这样：

```
a = b * 2;
```


The characters a and b are called variables (see "Variables"), which are like simple boxes you can store any of your stuff in. In programs, variables hold values (like the number 42) to be used by the program. Think of them as symbolic placeholders for the values themselves.

字符a和b被称之为变量，就像是一个你能存储任何东西在里面的盒子。在程序中，变量存放值(像数字42)来给程序用。将他们看做值本身的符号占位符。

By contrast, the 2 is just a value itself, called a literal value, because it stands alone without being stored in a variable.

相比之下，2就是这个值的本身，称之为字面量。因为它独立存在没有存在任何变量中。

The = and * characters are operators (see "Operators") -- they perform actions with the values and variables such as assignment and mathematic multiplication.

=和*字符是操作符 -- 他们使用值和变量执行运算相比如赋值和乘法运算。

Most statements in JavaScript conclude with a semicolon (;) at the end.

大多javascript声明的结尾带有;号。

The statement a = b * 2; tells the computer, roughly, to get the current value stored in the variable b, multiply that value by 2, then store the result back into another variable we call a.
a = b *2声明告诉计算机，概略的是，获取当前值存储在变量b中，乘2，然后存储到我们称之为a的变量中。


Programs are just collections of many such statements, which together describe all the steps that it takes to perform your program's purpose.

程序就是有相当多的声明，这些声明一同描述了它执行你程序目的的所有步骤。


## Expressions

Statements are made up of one or more expressions. An expression is any reference to a variable or value, or a set of variable(s) and value(s) combined with operators.

声明是由一个或多个表达式构成的。

For example:

```
a = b * 2;
```
This statement has four expressions in it:

这个声明有四个表达式：

2 is a literal value expression

2是一个字面量表达式

b is a variable expression, which means to retrieve its current value

b是一个变量表达式，它检索当前的值


b * 2 is an arithmetic expression, which means to do the multiplication

b * 2 是一个算术表达式，意味着乘法

a = b * 2 is an assignment expression, which means to assign the result of the b * 2 expression to the variable a (more on assignments later)

a = b * 2是一个任务表达式，以为着b * 2表达式的结果存储到变量a上

A general expression that stands alone is also called an expression statement, such as the following:

一般表达式独立存在的也称之为表达式语句，例如下面的


b * 2;
This flavor of expression statement is not very common or useful, as generally it wouldn't have any effect on the running of the program -- it would retrieve the value of b and multiply it by 2, but then wouldn't do anything with that result.
这种风格的表达式语句不是很常见和有效，运行这个程序通常不会产生任何影响 -- 它将会检索b的值然后乘2，但是不会对结果做任何处理

A more common expression statement is a call expression statement (see "Functions"), as the entire statement is the function call expression itself:

一个最常见的声明语句是调用表达式语句(参见函数)，整个表达式语句被称之为函数它自己。
```
alert( a );
```
## Executing a Program

How do those collections of programming statements tell the computer what to do? The program needs to be executed, also referred to as running the program.

如何通过这些收集的程序语句来告诉计算机做什么？程序需要被执行，也被称为运行项目。

Statements like a = b * 2 are helpful for developers when reading and writing, but are not actually in a form the computer can directly understand. So a special utility on the computer (either an interpreter or a compiler) is used to translate the code you write into commands a computer can understand.

在阅读和编写时像`a = b *2`这样的语句对于开发者来说是有帮助的，但是事实上计算机不能直接理解。所以在计算机中(也可以是 一个翻译者 或 编译者)一个特殊的工具被用来翻译你写的代码转变成计算机能够理解的命令。

For some computer languages, this translation of commands is typically done from top to bottom, line by line, every time the program is run, which is usually called interpreting the code.

对于一些计算机语言，翻译命令通常是从上至下翻译，一行一行向下，每次运行程序，通常被称之为解析代码。


For other languages, the translation is done ahead of time, called compiling the code, so when the program runs later, what's running is actually the already compiled computer instructions ready to go.

对于一些其他语言，提前翻译完成，称之为编译代码，所以当程序稍后运行时，他运行的实际上是已经编译完成能够运行的计算机结构。


It's typically asserted that JavaScript is interpreted, because your JavaScript source code is processed each time it's run. But that's not entirely accurate. The JavaScript engine actually compiles the program on the fly and then immediately runs the compiled code.

一般宣称JavaScript为解释性语言，因为每次运行JavaScript源码是都会处理它。但是不是完全精准，JavaScript引擎动态编译代码，并且立即运行编译的代码。

Note: For more information on JavaScript compiling, see the first two chapters of the Scope & Closures title of this series.

笔记：更多关于JavaScript的编译信息，看这一系列的作用域 & 闭包的标题的前两章。

##Try It Yourself

This chapter is going to introduce each programming concept with simple snippets of code, all written in JavaScript (obviously!).

这一章是使用简单的一段代码来讲述每一段程序的概念，所有使用代码JavaScript编写的(显而易见的！)

It cannot be emphasized enough: while you go through this chapter -- and you may need to spend the time to go over it several times -- you should practice each of these concepts by typing the code yourself. The easiest way to do that is to open up the developer tools console in your nearest browser (Firefox, Chrome, IE, etc.).

这一点无论如何强调都不过分： 当你开始阅读这一章 -- 并且你可能需要花一些时间去反复阅读它。你应该通过编写代码来锻炼这些概念。最简单的方式是打开最近的浏览器的开发者工具(火狐、谷歌、Ie，其他)

Tip: Typically, you can launch the developer console with a keyboard shortcut or from a menu item. For more detailed information about launching and using the console in your favorite browser, see "Mastering The Developer Tools Console" (http://blog.teamtreehouse.com/mastering-developer-tools-console). To type multiple lines into the console at once, use <shift> + <enter> to move to the next new line. Once you hit <enter> by itself, the console will run everything you've just typed.

提示：通常，你可以通过键盘的快捷键或者菜单选项打开开发者输入台，更多关于在你最喜欢的浏览器中打开和使用控制台，请看“掌握开发者控制台” (http://blog.teamtreehouse.com/mastering-developer-tools-console)，一次在控制台中输入多行，使用<shift> + <enter> 移动光标到下一行，一旦你按下回车，控制台将会运行你输入的一切。

Let's get familiar with the process of running code in the console. First, I suggest opening up an empty tab in your browser. I prefer to do this by typing about:blank into the address bar. Then, make sure your developer console is open, as we just mentioned.

让我们熟悉一下在控台内代码运行的过程。首先，我建议你在你的浏览器上打开一个新的标签，我更喜欢在地址栏输入`about:blank`，然后，确保你的开发者控制台是打开的，就像我们刚才提及的那样。

Now, type this code and see how it runs:

现在，输入这段代码然后看它执行：

a = 21;

b = a * 2;

console.log( b );
Typing the preceding code into the console in Chrome should produce something like the following:

输入过程之前的代码到谷歌控制台应该产生一些向下面的事情：


Go on, try it. The best way to learn programming is to start coding!

继续，试试看。学习程序最好的方法是开始编码。


## Output

In the previous code snippet, we used console.log(..). Briefly, let's look at what that line of code is all about.

在先前的代码片段，我们使用了console.log(..).短暂的，让我们寻找一下这一行代码是关于什么的。

You may have guessed, but that's exactly how we print text (aka output to the user) in the developer console. There are two characteristics of that statement that we should explain.

你可能已经猜到了，但是那正是我们如何在开发者控制台中打印文本(输入用户名)，我们应该解释这个语句中的那两个字符。

First, the log( b ) part is referred to as a function call (see "Functions"). What's happening is we're handing the b variable to that function, which asks it to take the value of b and print it to the console.

首先，这个log(b)部分被称为函数(看 "函数")。我们将变量b交给这个函数发生了什么，这个函数要求它取b的值并且打印在控制台上。

Second, the console. part is an object reference where the log(..) function is located. We cover objects and their properties in more detail in Chapter 2.

第二，`console.`部分是位于`log(..)`函数部分对象的引用，我们在第二章介绍了对象和他们属性更多的细节。

Another way of creating output that you can see is to run an alert(..) statement. For example:

你能看到其他方式创建输出语句是使用`alert()`语句。例如：

alert( b );
If you run that, you'll notice that instead of printing the output to the console, it shows a popup "OK" box with the contents of the b variable. However, using console.log(..) is generally going to make learning about coding and running your programs in the console easier than using alert(..), because you can output many values at once without interrupting the browser interface.

如果你运行这段代码，你将会注意到它代替了输出在控制台上,它显示一个弹出的“ok”框带有变量b的内容。然而，通常使用`console.log(..)`学习关于编程和运行程序比使用`alert(..)`更容易，因为你可以一次性输出很多值并且不会中断页面。

For this book, we'll use console.log(..) for output.

对于本书，我们使用`console.log(..)`来输出


##Input

While we're discussing output, you may also wonder about input (i.e., receiving information from the user).

当我们在讨论输出时，你可能也想要知道输入(接收用户的信息)

The most common way that happens is for the HTML page to show form elements (like text boxes) to a user that they can type into, and then using JS to read those values into your program's variables.

发生这种最常见的方式是HTML页面展示表单元素(想文本输入框)给用户输入，然后使用JS去读取这些变量到你程序的变量中。

But there's an easier way to get input for simple learning and demonstration purposes such as what you'll be doing throughout this book. Use the prompt(..) function:

但是最简单方式的获取用户输入对于简单的学习和演示目的，比如你将要通过本书来做的。使用`prompt(..)`函数：

age = prompt( "Please tell me your age:" );

console.log( age );
As you may have guessed, the message you pass to prompt(..) -- in this case, "Please tell me your age:" -- is printed into the popup.

你可能已经猜到了，你输入到`prompt(..)`的信息 --在这个案例里。“请告诉我你的名字：” -- 打印在这个弹窗上。

This should look similar to the following:

看起来跟下列的很相似：

Once you submit the input text by clicking "OK," you'll observe that the value you typed is stored in the age variable, which we then output with console.log(..):

一旦你通过点击“ok”来提交输入文本，你将会观察到你输入的将会存储到age变量中，然后我们通过`console.log(..)`输出变量

To keep things simple while we're learning basic programming concepts, the examples in this book will not require input. But now that you've seen how to use prompt(..), if you want to challenge yourself you can try to use input in your explorations of the examples.

当我们学习基础程序概念时保持简单，在这本书的案例中将不需要输入。但是现在你已经知道如何使用`prompt(..)`，如果你想要挑战你自己你可以尝试使用input来探索这个案例。

## Operators

Operators are how we perform actions on variables and values. We've already seen two JavaScript operators, the = and the *.

操作符是我们如何操作变量和值，我们已经看到两个JavaScript操作符，=号和*号。

The * operator performs mathematic multiplication. Simple enough, right?

*号操作符执行数学乘法运算，很简单对吗？

The = equals operator is used for assignment -- we first calculate the value on the right-hand side (source value) of the = and then put it into the variable that we specify on the left-hand side (target variable).

=号操作符通常用来复制-- 我们首先计算等号右边的值然后将值=号左边的变量中(目标变量).

Warning: This may seem like a strange reverse order to specify assignment. Instead of a = 42, some might prefer to flip the order so the source value is on the left and the target variable is on the right, like 42 -> a (this is not valid JavaScript!). Unfortunately, the a = 42 ordered form, and similar variations, is quite prevalent in modern programming languages. If it feels unnatural, just spend some time rehearsing that ordering in your mind to get accustomed to it.



Consider:

a = 2;
b = a + 1;
Here, we assign the 2 value to the a variable. Then, we get the value of the a variable (still 2), add 1 to it resulting in the value 3, then store that value in the b variable.

While not technically an operator, you'll need the keyword var in every program, as it's the primary way you declare (aka create) variables (see "Variables").

You should always declare the variable by name before you use it. But you only need to declare a variable once for each scope (see "Scope"); it can be used as many times after that as needed. For example:

var a = 20;

a = a + 1;
a = a * 2;

console.log( a );	// 42
Here are some of the most common operators in JavaScript:

Assignment: = as in a = 2.

Math: + (addition), - (subtraction), * (multiplication), and / (division), as in a * 3.

Compound Assignment: +=, -=, *=, and /= are compound operators that combine a math operation with assignment, as in a += 2 (same as a = a + 2).

Increment/Decrement: ++ (increment), -- (decrement), as in a++ (similar to a = a + 1).

Object Property Access: . as in console.log().

Objects are values that hold other values at specific named locations called properties. obj.a means an object value called obj with a property of the name a. Properties can alternatively be accessed as obj["a"]. See Chapter 2.

Equality: == (loose-equals), === (strict-equals), != (loose not-equals), !== (strict not-equals), as in a == b.

See "Values & Types" and Chapter 2.

Comparison: < (less than), > (greater than), <= (less than or loose-equals), >= (greater than or loose-equals), as in a <= b.

See "Values & Types" and Chapter 2.

Logical: && (and), || (or), as in a || b that selects either a or b.

These operators are used to express compound conditionals (see "Conditionals"), like if either a or b is true.

Note: For much more detail, and coverage of operators not mentioned here, see the Mozilla Developer Network (MDN)'s "Expressions and Operators" (https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators).

Values & Types
If you ask an employee at a phone store how much a certain phone costs, and they say "ninety-nine, ninety-nine" (i.e., $99.99), they're giving you an actual numeric dollar figure that represents what you'll need to pay (plus taxes) to buy it. If you want to buy two of those phones, you can easily do the mental math to double that value to get $199.98 for your base cost.

If that same employee picks up another similar phone but says it's "free" (perhaps with air quotes), they're not giving you a number, but instead another kind of representation of your expected cost ($0.00) -- the word "free."

When you later ask if the phone includes a charger, that answer could only have been either "yes" or "no."

In very similar ways, when you express values in a program, you choose different representations for those values based on what you plan to do with them.

These different representations for values are called types in programming terminology. JavaScript has built-in types for each of these so called primitive values:

When you need to do math, you want a number.
When you need to print a value on the screen, you need a string (one or more characters, words, sentences).
When you need to make a decision in your program, you need a boolean (true or false).
Values that are included directly in the source code are called literals. string literals are surrounded by double quotes "..." or single quotes ('...') -- the only difference is stylistic preference. number and boolean literals are just presented as is (i.e., 42, true, etc.).

Consider:

"I am a string";
'I am also a string';

42;

true;
false;
Beyond string/number/boolean value types, it's common for programming languages to provide arrays, objects, functions, and more. We'll cover much more about values and types throughout this chapter and the next.

Converting Between Types
If you have a number but need to print it on the screen, you need to convert the value to a string, and in JavaScript this conversion is called "coercion." Similarly, if someone enters a series of numeric characters into a form on an ecommerce page, that's a string, but if you need to then use that value to do math operations, you need to coerce it to a number.

JavaScript provides several different facilities for forcibly coercing between types. For example:

var a = "42";
var b = Number( a );

console.log( a );	// "42"
console.log( b );	// 42
Using Number(..) (a built-in function) as shown is an explicit coercion from any other type to the number type. That should be pretty straightforward.

But a controversial topic is what happens when you try to compare two values that are not already of the same type, which would require implicit coercion.

When comparing the string "99.99" to the number 99.99, most people would agree they are equivalent. But they're not exactly the same, are they? It's the same value in two different representations, two different types. You could say they're "loosely equal," couldn't you?

To help you out in these common situations, JavaScript will sometimes kick in and implicitly coerce values to the matching types.

So if you use the == loose equals operator to make the comparison "99.99" == 99.99, JavaScript will convert the left-hand side "99.99" to its number equivalent 99.99. The comparison then becomes 99.99 == 99.99, which is of course true.

While designed to help you, implicit coercion can create confusion if you haven't taken the time to learn the rules that govern its behavior. Most JS developers never have, so the common feeling is that implicit coercion is confusing and harms programs with unexpected bugs, and should thus be avoided. It's even sometimes called a flaw in the design of the language.

However, implicit coercion is a mechanism that can be learned, and moreover should be learned by anyone wishing to take JavaScript programming seriously. Not only is it not confusing once you learn the rules, it can actually make your programs better! The effort is well worth it.

Note: For more information on coercion, see Chapter 2 of this title and Chapter 4 of the Types & Grammar title of this series.

