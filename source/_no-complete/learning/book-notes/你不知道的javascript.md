# 你不知道的this与对象原型


## this

> 为什么要使用this

**我们先来看一段代码**

可以看出我们允许**identify**、**speak**函数对多个环境变量进行复用，而不是为了每个环境变量制作对应的函数

```
function identify() {
    return this.name.toUpperCase();
}
function speak() {
    var greeting = "Hello, I'm " + identify.call( this );
    console.log( greeting );
}
var me = {
    name: "Kyle"
};
var you = {
    name: "Reader"
};
identify.call( me ); // KYLE
identify.call( you ); // READER
speak.call( me ); // Hello, I'm KYLE
speak.call( you ); // Hello, I'm READER
```


**明确的将环境变量传递给函数**使用的模式越复杂，将执行环境当做明·确参数传递时，通常比this执行环境要乱

```
var you = {
    name: "Reader"
};

function identify(you) {
    return you.name.toUpperCase();
}
identify(you)
```

> this如何工作

this不是编写时绑定，而是运行时绑定。它依赖于函数调用的上下文，于函数申明的位置没有任何关系。而是与函数调用的方式紧密相连

函数在被调用时，会创建一个执行记录信息，这个记录包含函数是在何处被调用的，是如何被调用的，被传递了什么参数信息。这个记录属性之一，就是在这个函数被执行期间将被this引用




