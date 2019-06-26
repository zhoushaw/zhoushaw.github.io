---
title: vue技术内幕-数据响应系统
date: 2019-06-17 21:21:35
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

> 函数$watch,接收两个参数(要观测的key，回调函数)

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
        console.log('name 值发生更改');
    },
    get () {
        console.log('读取了属性name');
    }
});
```

通过`defineProperty`定义我们劫持了data对象的name属性操作，我们可以将劫持的方法封装至`watch`方法中，如下：


```
const data = {
    name: 'shaw'
};
$watch = function (key, fn) {
    Object.defineProperty(data,'name', {
        set (newValue) {
            fn();
        },
        get () {
            console.log('读取了属性name');
        }
    });
}
```

上面的代码已经简单实现了对数据的观测，但是大家不难发现其中存在的问题，上面例子中`set`函数并未设置属性新的赋值，并且`get`函数并未返回获取的值会导致属性的设置和获取失效。并且上面的例子，我们我无法对一个对象的属性收集多个依赖，并且我们每次调用`watch`都对属性重新定义了`set`和`get`,当属性还存在其他依赖时这样会覆盖原有的依赖，我们不妨展开🤔，`set`函数可以用于触发数据数据发生变化，我们可不可以通过`get`函数来进行依赖收集呢

```
var data = {
    name: 'shaw',
    age: 23
};

let Target;

let dep = [];

let val = data['name'];
Object.defineProperty(data, 'name', {
    set(newValue) {
        // 设置新值与旧值相等，不进行依赖
        if (val === newValue) return;
        val = newValue
        // 执行依赖
        dep.forEach(fn => fn());
    },
    get() {
        // 有依赖进行收集
        if (Target) dep.push(Target);
        return val;
    }
});

$watch = function (key,fn) {
    Target = fn;
    data[key];
}

$watch('name', () => {
    console.log('设置了name');
})

$watch('name', () => {
    console.log('多重依赖，啦啦啦');
})

data.name = 'zhou shaw';
```

上述代码并未对其`data`属性进行数据响应，我们可以通过遍历添加依赖关系。并且我们会发现若我们通过访问数据便收集了依赖，那么会触发大量的重复依赖收集后面我们会讲解如何解决：

```
var data = {
    name: 'shaw',
    age: 23
};

let Target; // 用于缓存依赖函数

for (let key in data) {
    let dep = [];
    let val = data[key];
    Object.defineProperty(data, key, {
        set(newValue) {
            if (val === newValue) return; // 设置新值与旧值相等，不进行依赖
            val = newValue
            dep.forEach(fn => fn()); // 执行依赖
        },
        get() {
            if (Target) dep.push(Target); // 有依赖进行收集
            return val;
        }
    });
}

let $watch = function (key,fn) {
    Target = fn;
    data[key];
}
```

但如果数据结构是这样呢：

```
var data = {
    name: 'shaw',
    infos: {
        phone: '17xxx',
        wechat: 'xxx'
    }
};
```

我们会发现我们并没有对深层次对象监听，如果数据结构更为复杂呢，我们可以将数据拦截方法封装成一个函数，对数据对象进行递归遍历，将所有属性都添加依赖，

```

let Target; // 用于缓存依赖函数

function walk(data) {
    for (let key in data) {
        let dep = [];
        let val = data[key];
        // 当数据为对象类型时递归遍历
        if (Object.prototype.toString.call(val) === '[object Object]') { 
            walk(val);
        }

        Object.defineProperty(data, key, {
            set(newValue) {
                if (val === newValue) return; // 设置新值与旧值相等，不进行依赖
                val = newValue
                dep.forEach(fn => fn()); // 执行依赖
            },
            get() {
                if (Target) dep.push(Target); // 有依赖进行收集
                return val;
            }
        });
    }
}

walk(data);

let $watch = function (key,fn) {
    Target = fn;
    data[key];
}
```

尽管对数据进行深度观察了，但我们会发现，我们的`watch`函数并不会对`infos.wechat`进行观察，所以我们需要对`$watch`函数进行改造，让其支持`infos.wechat`依赖收集，所以我们想实现的效果是：

```
$watch('infos.wechat', () => {
    console.log('修改了wechat');
})
```

由于我们已经实现了数据进行访问即可收集依赖，但我们无法直接通过`infos.wechat`收集，我们需要将其转换成`data['infos']['wechat']`

```
var data = {
    name: 'shaw',
    infos: {
        wechat: '466'
    }
};

let $watch = function (key,fn) {

    Target = fn;

    if (/\./.test(key)) {
        let paths = key.split('.');
        let obj = data;
        paths.forEach((path) => {
            obj = obj[path];
        });
        return;
    }

    data[key];
}
```

到这里为止我们已经实现了一个简单的数据依赖收集系统，我们如何实现dom节点和数据绑定式渲染呢，在vue中模板最终都会生成一个render函数，通过这个函数来实现最终的渲染。若`render`函数中访问了`data`数据，我们可以观察`render`函数中的data数据，若`render`函数中访问的数据发生变化，则执行`render`函数进行重新渲染，那么如何收集`render`函数中访问的依赖，并将`render`函数与数据建立联系呢，很简单我们将`watch`函数进行改造一下就行了

```
let $watch = function (exp,fn) {

    Target = fn;
    if (typeof exp==="function") {
        exp();
        return;
    }

    if (/\./.test(exp)) {
        let paths = exp.split('.');
        let obj = data;
        paths.forEach((path) => {
            obj = obj[path];
        });
        return;
    }

    data[exp];
}

function render() {
    return document.write(`姓名：${data.name}; 年龄：${data.age}<br/>`)
}

$watch(render, render)
```

在这里我们将`$watch`函数进行了改造，我们将第一个参数的表达是进行了类型判断，如果是函数类型进行执行。因为我们是通过`get`拦截进行依赖收集的，执行函数后可以收集`render`函数中数据的依赖，依赖的执行函数就是`render`，若我们对`render`函数中依赖的data数据进行修改，就会触发`render`函数从而实现数据响应视图。当然这里的实现只是vue的基本原理，从这里我们不难看出我们实现的这个简陋的响应系统中存在的问题，当修改数据触发`render`函数时，又进行了重复的依赖收集，并且这里也没有针对`Object.defineProperty`属性无法对数组进行观察进行处理。接下来会针对这一系列问题进行处理





