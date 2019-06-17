---
title: vue技术内幕-数据响应系统
date: 2019-06-17 9:21:35
tags: vue
categories: vue
---


## 数据响应系统的基本思路

我们都知道在`Vue`中存在`watch`(观察者)。通过设置`watch`可以对数据进行观察，当数据发生变化时，可以执行对应的观察函数，下面为例：

```
var ins = new Vue({
    data () {
        return {
            name: 'shaw'
        }
    }
})
ins.$watch('name', ()=>{
    console.log('name数据发生修改');
});
```

在这个例子中，当我们使用`ins.name='zhou shaw'`进行修改数据时，控制台会输出`name数据发生修改`,现在我们将功能抽象出来：

> 假设我们有一个数据data

```
const data = {
    name: 'shaw'
};

```

> 函数$watch,接收两个参数，要观测的key，和回调函数

```
$watch(key,()=>{...})
```

> 实现的抽象功能


```
const data = {
    name: 'shaw'
};
$watch('name',()=>{
    console.log('name 值发生更改');
});

data.name = 'zhou shaw';
# log： name 值发生更改
```

我们通过`$watch`函数来添加`data`对象数据的依赖关系，若`data`中的数据发生改变时出发对应`watch`函数。实现这样一个功能说复杂也复杂说简单也简单，说复杂是因为我们需要考虑到很多便捷情况、如重复依赖、深度观测，以及如何处理数组等多种情况。我们暂且不考虑这些边界情况，来实现一个简单的响应式系统。


首先我们需要面临的第一个问题就是，如何检测数据发生了变化，我们可以通过`Object.defineProperty`来对属性进行检测：

```
const data = {
    name: 'shaw'
};
Object.defineProperty(data,'name', {
    set (newValue) {
        data.value = newValue;
        console.log('name 值发生更改');
    },
    get () {
        console.log('读取了属性name')
    }
});
```

通过`defineProperty`定义name的设置和获取操作，我们不妨大胆的想象一下，我们可以通过`get`操作添加

