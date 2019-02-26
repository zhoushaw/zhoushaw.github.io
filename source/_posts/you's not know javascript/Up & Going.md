---
title: 译文：you don't know js 至 Into YDKJS
date: 2019-02-26 10:42:35
tags: book
categories: js
---


<div><!-- more--></div>

# Chapter 3: Into YDKJS

What is this series all about? Put simply, it's about taking seriously the task of learning all parts of JavaScript, not just some subset of the language that someone called "the good parts," and not just whatever minimal amount you need to get your job done at work.

这一系列书主要用于谈论什么呢？简单来说，这一系列书主要用户讲述如何学好javascript，而不是学习一些人称之为javascript中好的部分，也不仅仅能让你搞定工作的那一小部分内容。

Serious developers in other languages expect to put in the effort to learn most or all of the language(s) they primarily write in, but JS developers seem to stand out from the crowd in the sense of typically not learning very much of the language. This is not a good thing, and it's not something we should continue to allow to be the norm.

在其他语言中，认真的开发者总是希望努力学习他们主要使用语言的大部分或全部。但JS开发者通常不太学习这门语言，而显得特别突出。这不是一件好事，我们也不应该将其视为常态。

The You Don't Know JS (YDKJS) series stands in stark(完全) contrast(对比) to the typical approaches to learning JS, and is unlike almost any other JS books you will read. It challenges you to go beyond your comfort zone(舒适区) and to ask the deeper "why" questions for every single behavior you encounter. Are you up for that challenge?

你不知道JS系列书籍与传统的学习JS方式大不相同，它也不像你所阅读的其他系列的JS书籍。它会使你遇到挑战逼迫你走出舒适区，对你遇到的每一个问题深入的问为什么。你准备好迎接挑战了吗？

I'm going to use this final chapter to briefly(短暂) summarize(总结) what to expect from the rest of the books in the series, and how to most effectively go about building a foundation of JS learning on top of(在...之上) YDKJS.

我将会用最后一章来做一个简短的总结，这一系列其他章节的内容，如何更有效的通过YDKJS建立学习JS的基础。

## 作用域 & 闭包

Perhaps one of the most fundamental things you'll need to quickly come to terms with is how scoping of variables really works in JavaScript. It's not enough to have anecdotal fuzzy beliefs about scope.

可能你最需要尽快明白的基本原理就是变量的作用域是如何在JS中工作的。仅仅只知道关于作用域模糊的概念是不够的。

The Scope & Closures title starts by debunking the common misconception that JS is an "interpreted language" and therefore not compiled. Nope.

作用域 & 闭包这一章节从揭示最常见的误解开始，JS是一门解释性语言，而不是被编译的。不对。

The JS engine compiles your code right before (and sometimes during!) execution. So we use some deeper understanding of the compiler's approach to our code to understand how it finds and deals with variable and function declarations. Along the way, we see the typical metaphor for JS variable scope management, "Hoisting."

JS引擎会对你的代码进行编译在你的代码执行之前(有时在执行时)。所以我们需要深入理解编译器处理我们代码的方式，以理解编译器如何找到并处理申明的变量和函数。沿着这条路，我们将见到js变量作用域管理特有的隐式提升。

This critical(批评的、决定性的) understanding of "lexical(词汇) scope" is what we then base our exploration of closure on for the last chapter of the book. Closure is perhaps the single most important concept in all of JS, but if you haven't first grasped(抓住、理会) firmly how scope works, closure will likely remain beyond your grasp.

理解作用域这一关键词是至关重要的，在最后一张它是我们理解和探索闭包的基础。闭包可能是js所有概念中最重要之一，但是如果你第一次没有完全理解作用域的工作原理，闭包将会超越你的理解。

One important application of closure is the module pattern, as we briefly introduced in this book in Chapter 2. The module pattern is perhaps the most prevalent code organization pattern in all of JavaScript; deep understanding of it should be one of your highest priorities.

模块模式是闭包中一个重要的应用，我们在本书第二章会将会介绍它的基础概念。模块模式可能是所有js流行代码组织的模式。深入理解它应该是你最优先做的事情。


## this & Object Prototypes

Perhaps one of the most widespread and persistent mistruths about JavaScript is that the this keyword refers to the function it appears in. Terribly mistaken.

可能关于JS最普遍最持久的谬论是关键词this指代的是它的所出现的函数。可怕的谬论。

The this keyword is dynamically bound based on how the function in question is executed, and it turns out there are four simple rules to understand and fully determine this binding.

关键词this的指向动态的基于函数是如何执行的，是这里有四个简单的规则去理解和选择this绑定。


Closely related to the this keyword is the object prototype mechanism, which is a look-up chain for properties, similar to how lexical scope variables are found. But wrapped up in the prototypes is the other huge miscue about JS: the idea of emulating (fake) classes and (so-called "prototypal") inheritance.

与this关键词密密相关的是object原型的原理，这是一个查找属性的链。与查询的方式相似。但是包含在原型中另一个JS的巨大谬论：模拟类和继承的想法

Unfortunately, the desire to bring class and inheritance design pattern thinking to JavaScript is just about the worst thing you could try to do, because while the syntax may trick you into thinking there's something like classes present, in fact the prototype mechanism is fundamentally opposite in its behavior.

不幸的是，渴望将类和继承设计模式的想法带入JS将是你做的最糟糕的事情，因为将这种语法会使你认为有类的功能的存在，事实上原型原来是与类的概念是完全相反的。


What's at issue is whether it's better to ignore the mismatch and pretend that what you're implementing is "inheritance," or whether it's more appropriate to learn and embrace how the object prototype system actually works. The latter is more appropriately named "behavior delegation."

问题是忽略它的不匹配并且假装是在完成继承是否是一件好事，或者学习并拥抱对象属性系统工作方式是否合适。后者被称为行为系统更合适。

This is more than syntactic preference. Delegation is an entirely different, and more powerful, design pattern, one that replaces the need to design with classes and inheritance. But these assertions will absolutely fly in the face of nearly every other blog post, book, and conference talk on the subject for the entirety of JavaScript's lifetime.

这不仅仅是语法上的偏好。委托是一种完全不同更强大的设计模式，一个可以替换了需要类和继承的设计。但是在javascript整个生命周期中在几乎所有博客的文章、书籍和会议讨论关于这个主题都是背道而驰的。

The claims I make regarding delegation versus inheritance come not from a dislike of the language and its syntax, but from the desire to see the true capability of the language properly leveraged and the endless confusion and frustration wiped away.

我对委托和继承做出的宣言不是源于对语言和其语法的厌恶，而是来自于渴望看到这门语言的真实力量被正确地利用，渴望看到无尽的困惑与沮丧被一扫而光。

But the case I make regarding prototypes and delegation is a much more involved one than what I will indulge here. If you're ready to reconsider everything you think you know about JavaScript "classes" and "inheritance," I offer you the chance to "take the red pill" (Matrix 1999) and check out Chapters 4-6 of the this & Object Prototypes title of this series.

但是我讲的关于原型和委托例子比我在这里讲的涉及的还要多。如果你准备好重新思考你所认为关于JS中的类和继承,我将会提供给你这个机会去思考并改变，然后你可以查阅这一系列的this & object prototype的第4-6章


## Types & Grammar

The third title in this series primarily focuses on tackling yet another highly controversial topic: type coercion. Perhaps no topic causes more frustration with JS developers than when you talk about the confusions surrounding implicit coercion.

在这一系列中的第三标题主要讨论另一个比较有争议的话题：强制类型转换。可能没有什么话题能比你讨论混乱的类型转换能让JS开发者更沮丧的话题了。

By far, the conventional wisdom is that implicit coercion is a "bad part" of the language and should be avoided at all costs. In fact, some have gone so far as to call it a "flaw" in the design of the language. Indeed, there are tools whose entire job is to do nothing but scan your code and complain if you're doing anything even remotely like coercion.

到目前为止，传统的智慧是既然强制类型转换是这门医院糟糕的部分，我们应当不计一切的成本去避免他。事实上，一些人去称之为语言坏的一部分。事实上，已经有很多专门扫描代码的工具，当你的代码中使用了强制类型转换或者类似强制转换的事情将会报警。

But is coercion really so confusing, so bad, so treacherous, that your code is doomed from the start if you use it?

但是强制类型真的如此混乱、如此糟糕、如此不可靠，以致于你在代码中使用它就导致你的代码走向灭亡了吗？

I say no. After having built up an understanding of how types and values really work in Chapters 1-3, Chapter 4 takes on this debate and fully explains how coercion works, in all its nooks and crevices. We see just what parts of coercion really are surprising and what parts actually make complete sense if given the time to learn.

不是的，不是这样的。在第1-3章中讲解了类型和值真实是如何工作的，第4章参与了这个讨论，并从全面的角度分析强制类型是如何工作的。如果你花时间去学习它的话你回对强制类型转换感到惊奇并且是十分完整的。

But I'm not merely suggesting that coercion is sensible and learnable, I'm asserting that coercion is an incredibly useful and totally underestimated tool that you should be using in your code. I'm saying that coercion, when used properly, not only works, but makes your code better. All the naysayers and doubters will surely scoff at such a position, but I believe it's one of the main keys to upping your JS game.

但是我不仅仅建议强制类型转换是明智的并且可学的，我声明强制类型转换是非常有用的，你应该使用你的代码而不是使用那些检测工具。我要说当你正常使用强制类型转换不仅仅可以工作还会使你的代码更好。所有的否定者和怀疑者毫无疑问将会嘲笑这个立场，但是我相信它将会是你玩好JS的主键之一。

Do you want to just keep following what the crowd says, or are you willing to set all the assumptions aside and look at coercion with a fresh perspective? The Types & Grammar title of this series will coerce your thinking.

你是否还是坚持相信大多数人所说的，或者是说你已经将所有的猜想都放到一边。并且对强制转换有了一个新的观点？类型和语法这一章将会强制转换你思考。


## Async & Performance

The first three titles of this series focus on the core mechanics of the language, but the fourth title branches out slightly to cover patterns on top of the language mechanics for managing asynchronous programming. Asynchrony is not only critical to the performance of our applications, it's increasingly becoming the critical factor in writability and maintainability.

这一系列的第三个标题我们将主要关注这门语言的核心技术，但是第四个标题稍微扩展了一些，以涵盖用于管理异步编程的语言机制之上的模式。一部不是唯一评判我们应用性能的标砖，越来越多的评判因素是根绝可写性和可维护性。

The book starts first by clearing up a lot of terminology and concept confusion around things like "async," "parallel," and "concurrent," and explains in depth how such things do and do not apply to JS.

这本书首次开始理清大量的属于和混乱的概念类似于：异步、同步、并行，深入的解释这些东西如何用或者不用再JS上。

Then we move into examining callbacks as the primary method of enabling asynchrony. But it's here that we quickly see that the callback alone is hopelessly insufficient for the modern demands of asynchronous programming. We identify two major deficiencies of callbacks-only coding: Inversion of Control (IoC) trust loss and lack of linear reason-ability.

然后我们将思考为什么回调作为主要的方法实现异步，但是我们将很快的看到回调对于异步编程来说，仅仅依靠回调是不够的。我们确定了回调代码的两个不足。控制反转(IoC)信任缺失，缺乏线性推理能力。

To address these two major deficiencies, ES6 introduces two new mechanisms (and indeed, patterns): promises and generators.

为了解决这两大不足，est介绍了两种技术：promise和generators

Promises are a time-independent wrapper around a "future value," which lets you reason about and compose them regardless of if the value is ready or not yet. Moreover, they effectively solve the IoC trust issues by routing callbacks through a trustable and composable promise mechanism.

promise是一个关于未来值的时间包装，它允许你组成并推理他们，无论值是否已准备好。并且，他们有效的解决了控制反转信任问题，通过可信任和可组合的promise机制路由回调。

Generators introduce a new mode of execution for JS functions, whereby the generator can be paused at yield points and be resumed asynchronously later. The pause-and-resume capability enables synchronous, sequential looking code in the generator to be processed asynchronously behind the scenes. By doing so, we address the non-linear, non-local-jump confusions of callbacks and thereby make our asynchronous code sync-looking so as to be more reason-able.

Generators介绍了一个行的JS函数执行模式，凭借generator能通过yield关键词暂停并且稍后重新开始异步。这种暂停和重新开始的异步能力，在后台异步处理生成器中的顺序查找代码。通过这样做，我们能处理回调函数的非线性、回调之间的混乱跳转。因此能够使我们的异步代码越来越同步和可靠。

But it's the combination of promises and generators that "yields" our most effective asynchronous coding pattern to date in JavaScript. In fact, much of the future sophistication of asynchrony coming in ES7 and later will certainly be built on this foundation. To be serious about programming effectively in an async world, you're going to need to get really comfortable with combining promises and generators.

但是yields结合了promise和generators是我们至今为止在JS中最有效的异步代码风格。事实上，不远将来，在es7或者后面版本中将会迎来更复杂的异步的，可以确定的是都将建立在这个基础之上。认真对待异步世界中的有效编程,你需要去适应promise和generator的混合。

If promises and generators are about expressing patterns that let our programs run more concurrently and thus get more processing accomplished in a shorter period, JS has many other facets of performance optimization worth exploring.

如果promise和generator是关于表达模式，使我们的程序能够更并发地运行，从而在更短的时间内完成更多的处理，JS有很多其他性能优化的内容值得探索。


Chapter 5 delves into topics like program parallelism with Web Workers and data parallelism with SIMD, as well as low-level optimization techniques like ASM.js. Chapter 6 takes a look at performance optimization from the perspective of proper benchmarking techniques, including what kinds of performance to worry about and what to ignore.
第五章将进入并行主题的web工作和并行数据的SIMD，与低级别的压缩技术想ASM.js。第六章从基准技术来看一看性能优化，包括哪些性能是需要担忧的哪些是可以忽略的。


Writing JavaScript effectively means writing code that can break the constraint barriers of being run dynamically in a wide range of browsers and other environments. It requires a lot of intricate and detailed planning and effort on our parts to take a program from "it works" to "it works well."

编写有效的javascript意味着编写能够打破能动态运行在大多数浏览器和其他环境的障碍。它能工作到它能工作的很好，需要很多复杂详细的计划和努力。

The Async & Performance title is designed to give you all the tools and skills you need to write reasonable and performant JavaScript code.

这异步和性能标题是为了给你需要编写合理和高性能的js代码所需要的工具和技能。

ES6 & Beyond
No matter how much you feel you've mastered JavaScript to this point, the truth is that JavaScript is never going to stop evolving, and moreover, the rate of evolution is increasing rapidly. This fact is almost a metaphor for the spirit of this series, to embrace that we'll never fully know every part of JS, because as soon as you master it all, there's going to be new stuff coming down the line that you'll need to learn.

无论你感觉你多精通javascript，真理是javascript绝不停止更新，而且，更新的速度变得越来越快。事实从这一系列去拥抱我们踊跃都不可能知道Js的所有部分，因为你不可能精通它所有的部分，很快就可能有新的功能你需要去学习的。


This title is dedicated to both the short- and mid-term visions of where the language is headed, not just the known stuff like ES6 but the likely stuff beyond.

这个标题是专注于这门语言短期和中期房展方向的，不仅仅知道es6这样的东西还有其他可能得东西

While all the titles of this series embrace the state of JavaScript at the time of this writing, which is mid-way through ES6 adoption, the primary focus in the series has been more on ES5. Now, we want to turn our attention to ES6, ES7, and ...

而本系列的所有标题包含了这一时期协作的javascript状态，哪些中等方法通过了es6的采用，着一些列主要关注更多的在于es5，现在我们将要转变我们的注意到es6、es7更多

Since ES6 is nearly complete at the time of this writing, ES6 & Beyond starts by dividing up the concrete stuff from the ES6 landscape into several key categories, including new syntax, new data structures (collections), and new processing capabilities and APIs. We cover each of these new ES6 features, in varying levels of detail, including reviewing details that are touched on in other books of this series.

因为在写作之时es6已经接近完成，es6和beyond开始分割es6功能为几个关键分类，包括新的预发，新的数据结果和新的处理能力和api。我们覆盖了所有新的es6功能，在不变的详细等级，包括在这一系列的其他书上触摸到的细节。

Some exciting ES6 things to look forward to reading about: destructuring, default parameter values, symbols, concise methods, computed properties, arrow functions, block scoping, promises, generators, iterators, modules, proxies, weakmaps, and much, much more! Phew, ES6 packs quite a punch!

一些令人兴奋盼望去阅读的es6事物：解构、参数默认值、符号、简单方法、计算属性、箭头函数、块作用域、承诺、生成器、遍历、模块化、代理。es6很有冲击力


The first part of the book is a roadmap for all the stuff you need to learn to get ready for the new and improved JavaScript you'll be writing and exploring over the next couple of years.

本书的第一部分是一张路线图，列出了你所有需要学习的内容。为了在未来几年编写和研究新的javascript内容和改进javascript做好准备。

The latter part of the book turns attention to briefly glance at things that we can likely expect to see in the near future of JavaScript. The most important realization here is that post-ES6, JS is likely going to evolve feature by feature rather than version by version, which means we can expect to see these near-future things coming much sooner than you might imagine.

本书的最后一部分转变注意力到，简单浏览一下在不远将来我们能在javascript中看到的内容。es6的发布是最重要的关系，JS看起来就像进入了一个功能接一个功能一个版本接一个版本。这意味着我们能探索的不远将来的事情很快就会到来，比你想象的还要快。

The future for JavaScript is bright. Isn't it time we start learning it!?

Javascript的未来是明亮的。现在不是我们开始学习的时候了吗？

Review
The YDKJS series is dedicated to the proposition that all JS developers can and should learn all of the parts of this great language. No person's opinion, no framework's assumptions, and no project's deadline should be the excuse for why you never learn and deeply understand JavaScript.

你不懂js系列是专注于所有JS开发者能并且应该学习这一伟大语言的所有部分的这一命题。没有个人之见，没有框架假设，没有项目期限能成为你为什么学习并且深入理解javascript的原因。

We take each important area of focus in the language and dedicate a short but very dense book to fully explore all the parts of it that you perhaps thought you knew but probably didn't fully.

我们谈论这门语言应该关注的重点地方并且致力于简短，但是非常浓密的书去充分探索有可能认为你知道倒是可能不全面的所有部分。

"You Don't Know JS" isn't a criticism or an insult. It's a realization that all of us, myself included, must come to terms with. Learning JavaScript isn't an end goal but a process. We don't know JavaScript, yet. But we will!

你不懂JS不是批评和侮辱。这是我们所有人人认知的，我自己也不例外。学习javascript不是一个最终目标但是是一个过程。我们不懂javascript，但是我们将会懂得。


