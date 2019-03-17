---
title: throttle 和 debounce
date: 2018-10-23 8:07:0
tags: js
categories: js
---

> throttle 和 debounce是控制频率的高阶函数，返回一个包装后的匿名函数

在实际工作中的很多场景下都会使用到这两个高阶函数，并且在javascript中利用了闭包这一特性。下面对这两个函数进行详细讲解
应用场景:

* resize 重新计算样式布局   --debounce
* input输入停止1s时，获取ajax请求     --debounce
* scroll 计算当前是否大于固定值，显示头部   --throttle
<div><!-- more--></div>


## throttle

throttle也可以称之为节流函数，主要用于控制一段时间内，只允许执行一次指定函数。类似于打开阀门的水龙头，每过固定的时间内，滴出不超过一滴水

主要场景用于:

* scroll
* resize
* mouse move

在我们的实际工作中，基于性能和效率上的考虑，要限制函数的执行频率可以使用throttle

以地铁为例进行说明:

某个函数去乘坐地铁，必须等待🚇到站后，才能上车。🚇到站函数可以上车，但在固定时间点后，不管有没有人继续上车，🚇将会发车。

在实际工作中的应用，列如:

淘宝网需要在用户滑动滚轮，距离顶部500px时，隐藏顶部导航栏，这个时候我们需要对用户的滑动事件进行监听，当用户进行滑动时，我们可以获取到用户当前滑动的距离，与500px进行比较。当用户的滑动距离大于等于500时，执行隐藏操作。

通常实现:

```
window.addEventListener("scroll", () => {
    let scrollTop = document.documentElement.scrollTop
    if (scrollTop >= 500) {
       // 隐藏头部逻辑
    }
})
```
但是滚动事件的触发频率非常高，这样将会造成性能上的浪费，我们可以通过throttle函数来控制频率，我们可以控制用户在滚动滚轮时，在500毫秒内只触发一次检测，当前用户距离是否距离顶部大于等于500

具体实现:


```
# throttle函数
function throttle(fn,delay = 250){
    let timer;
    let last;
    
    return function () {
        let now = +new Date();
        if (last && last + delay > now) {
            clearTimeout(timer);
            timer = setTimeout(function () {
                last = now;
                fn.apply(this, arguments);
            },delay)
        } else {
            last = now;
            fn.apply(this, arguments);
        }
    }
}
```


## debounce


debounce更类似于按压的弹簧，当你用力按压时，弹簧是不会弹起的。也可以比喻成电梯，电梯在一层停留时，只要有人进入就会一直陷入等待进入状态，等到没有人进入时就会移动。

例:

```
以输入框的输入事件为例，淘宝网有一个银行卡添加页面，当用户在输入框输入银行卡时，会通过ajax请求获取当前银行卡类型，并检测是否支持。若用户每输入一个数字就进行校验，会造成性能上的浪费，可以通过debounce防抖函数，设置用户停止输入一秒后，对银行卡进行校验识别。
```

具体实现:


```
function debounce(fn, delay = 1000) {
    var timer;
    var context = this;
    return function() {
        if (timer) {
            clearTimeout(timer);
            timer = setTimeout(function() {
                fn.apply(context,arguments);
            }, delay)
        } else {
            timer = setTimeout(function() {
                fn.apply(context,arguments);
            }, delay)
        }
    }
}
```


