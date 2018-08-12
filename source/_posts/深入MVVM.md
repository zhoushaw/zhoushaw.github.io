---
title: 深入MVVM
date: 2018-03-17 7:52:35
tags: vue
categories: vue
---


MVVM框架大行其道，这么炫酷的视图渲染模式。骚年有没有兴趣一起了解一波，那就让我们一起开始吧_(:з」∠)

<div><!-- more--></div>

## Object.defineProperty

> 在了解双向绑定原理之前我们先了解一个重要的属性Object.defineProperty

该方法可以用于定义数据可修改性、可否遍历，已经设定属性读取时触发对应的函数

```javascript
Object.defineProperty(obj,'a',{
    get: function(){
        // 该函数在访问该属性时，被调用
        return '获取到这个值啦，哈哈哈';
    },
    set: function(newValue){
        console.log('你要赋新的值给我啊，哈哈.并且这个值是',newValue)
    },
    enumerable: false,// 设置为false之后该属性不可以被遍历读取
    configurable: false,//设置configurable为false之后，该属性不可以再使用defineProperty重新对该属性定义
    // writable: true,// 设置writeable之后，设置的属性不可以改写
    // value: 'hello world'
});
// 不能 同时设置访问器 (get 和 set) 和 wriable 或 value
// 默认该三个属性都为false
obj.a = 'hello';
```

> get函数

该函数在属性被访问时触发，返回值是获取到的值

例：
```javascript
var obj = {
    a: 'hello world'
};
Object.defineProperty(obj,'a',{
    get: function(){
        return '你想要获取obj的a属性值是吗'
    }
})

console.log(obj.a);// 输出你想要获取obj的a属性值是吗
```

> setter函数

该函数在属性被写入时触发
例：
```javascript
var obj = {
    a: 'hello world'
};
Object.defineProperty(obj,'a',{
    set: function(){
        console.log('你在给a属性设置新值')
    }
})

obj.a = 'good byes world'// 你在给a属性设置新值
```

enumerable: false,// 设置为false之后该属性不可以被遍历读取
configurable: false,//设置configurable为false之后，该属性不可以再使用defineProperty重新对该属性定义
writable: true,// 设置writeable之后，设置的属性不可以改写
value: 'hello world'// 获取该值时，返回value内容，value不可以与set或get函数同时存在

## 实现思路

了解实现核心概念后，我们一起来了解一下总体实现思路

### 要实现mvvm的双向绑定，就必须要实现以下几点

实现一个数据监听器Observer，能够对数据对象的所有属性进行监听，如有变动可拿到最新值并通知订阅者
实现一个指令解析器Compile，对每个元素节点的指令进行扫描和解析，根据指令模板替换数据，以及绑定相应的更新函数
实现一个Watcher，作为连接Observer和Compile的桥梁，能够订阅并收到每个属性变动的通知，执行指令绑定的相应回调函数，从而更新视图
mvvm入口函数，整合以上三者

上述流程如图所示：

![2](media/2.png)

### 实现Observer

- 我们知道可以利用Obeject.defineProperty()来监听属性变动
- 那么将需要observe的数据对象进行递归遍历，包括子属性对象的属性，都加上setter和getter
- 这样的话，给这个对象的某个值赋值，就会触发setter，那么就能监听到了数据变化。相关代码可以是这样

```
var data = {name: 'kindeng'};
observe(data);
data.name = 'dmq'; // 哈哈哈，监听到值变化了 kindeng --> dmq

function observe(data) {
    if (!data || typeof data !== 'object') {
        return;
    }
    // 取出所有属性遍历
    Object.keys(data).forEach(function(key) {
	    defineReactive(data, key, data[key]);
	});
};

function defineReactive(data, key, val) {
    observe(val); // 监听子属性
    Object.defineProperty(data, key, {
        enumerable: true, // 可枚举
        configurable: false, // 不能再define
        get: function() {
            return val;
        },
        set: function(newVal) {
            console.log('哈哈哈，监听到值变化了 ', val, ' --> ', newVal);
            val = newVal;
        }
    });
}
```

> 这样我们已经可以监听每个数据的变化了，那么监听到变化之后就是怎么通知订阅者了，所以接下来我们需要实现一个消息订阅器，很简单，维护一个数组，用来收集订阅者，数据变动触发notify，再调用订阅者的update方法，代码改善之后是这样

```
// ... 省略
function defineReactive(data, key, val) {
	var dep = new Dep();
    observe(val); // 监听子属性

    Object.defineProperty(data, key, {
        // ... 省略
        set: function(newVal) {
        	if (val === newVal) return;
            console.log('哈哈哈，监听到值变化了 ', val, ' --> ', newVal);
            val = newVal;
            dep.notify(); // 通知所有订阅者
        }
    });
}

function Dep() {
    this.subs = [];
}
Dep.prototype = {
    addSub: function(sub) {
        this.subs.push(sub);
    },
    notify: function() {
        this.subs.forEach(function(sub) {
            sub.update();
        });
    }
};
```

- 那么问题来了，谁是订阅者，怎么往订阅器添加订阅者？
- 没错，上面的思路整理中我们已经明确订阅者应该是Watcher, 而且var dep = new Dep();是在 defineReactive方法内部定义的，所以想通过dep添加订阅者，就必须要在闭包内操作，所以我们可以在getter里面动手脚：


```
// Observer.js
// ...省略
Object.defineProperty(data, key, {
	get: function() {
		// 由于需要在闭包内添加watcher，所以通过Dep定义一个全局target属性，暂存watcher, 添加完移除
		Dep.target && dep.addDep(Dep.target);
		return val;
	}
    // ... 省略
});

// Watcher.js
Watcher.prototype = {
	get: function(key) {
		Dep.target = this;
		this.value = data[key];	// 这里会触发属性的getter，从而添加订阅者
		Dep.target = null;
	}
}
```

- 这里已经实现了一个Observer了，已经具备了监听数据和数据变化通知订阅者的功能。那么接下来就是实现Compile了

> 实现Compile

- compile主要做的事情是解析模板指令，将模板中的变量替换成数据，然后初始化渲染页面视图
- 并将每个指令对应的节点绑定更新函数，添加监听数据的订阅者，一旦数据有变动，收到通知，更新视图，如图所示

因为遍历解析的过程有多次操作dom节点，为提高性能和效率，会先将跟节点el转换成文档碎片fragment进行解析编译操作
解析完成，再将fragment添加回原来的真实dom节点中

![3](media/3.png)


```
function Compile(el) {
    this.$el = this.isElementNode(el) ? el : document.querySelector(el);
    if (this.$el) {
        this.$fragment = this.node2Fragment(this.$el);
        this.init();
        this.$el.appendChild(this.$fragment);
    }
}
Compile.prototype = {
	init: function() { this.compileElement(this.$fragment); },
    node2Fragment: function(el) {
        var fragment = document.createDocumentFragment(), child;
        // 将原生节点拷贝到fragment
        while (child = el.firstChild) {
            fragment.appendChild(child);
        }
        return fragment;
    }
};
```

- compileElement方法将遍历所有节点及其子节点，进行扫描解析编译，调用对应的指令渲染函数进行数据渲染，并调用对应的指令更新函数进行绑定，详看代码及注释说明


```
Compile.prototype = {
	// ... 省略
	compileElement: function(el) {
        var childNodes = el.childNodes, me = this;
        [].slice.call(childNodes).forEach(function(node) {
            var text = node.textContent;
            var reg = /\{\{(.*)\}\}/;	// 表达式文本
            // 按元素节点方式编译
            if (me.isElementNode(node)) {
                me.compile(node);
            } else if (me.isTextNode(node) && reg.test(text)) {
                me.compileText(node, RegExp.$1);
            }
            // 遍历编译子节点
            if (node.childNodes && node.childNodes.length) {
                me.compileElement(node);
            }
        });
    },

    compile: function(node) {
        var nodeAttrs = node.attributes, me = this;
        [].slice.call(nodeAttrs).forEach(function(attr) {
            // 规定：指令以 v-xxx 命名
            // 如 <span v-text="content"></span> 中指令为 v-text
            var attrName = attr.name;	// v-text
            if (me.isDirective(attrName)) {
                var exp = attr.value; // content
                var dir = attrName.substring(2);	// text
                if (me.isEventDirective(dir)) {
                	// 事件指令, 如 v-on:click
                    compileUtil.eventHandler(node, me.$vm, exp, dir);
                } else {
                	// 普通指令
                    compileUtil[dir] && compileUtil[dir](node, me.$vm, exp);
                }
            }
        });
    }
};

// 指令处理集合
var compileUtil = {
    text: function(node, vm, exp) {
        this.bind(node, vm, exp, 'text');
    },
    // ...省略
    bind: function(node, vm, exp, dir) {
        var updaterFn = updater[dir + 'Updater'];
        // 第一次初始化视图
        updaterFn && updaterFn(node, vm[exp]);
        // 实例化订阅者，此操作会在对应的属性消息订阅器中添加了该订阅者watcher
        new Watcher(vm, exp, function(value, oldValue) {
        	// 一旦属性值有变化，会收到通知执行此更新函数，更新视图
            updaterFn && updaterFn(node, value, oldValue);
        });
    }
};

// 更新函数
var updater = {
    textUpdater: function(node, value) {
        node.textContent = typeof value == 'undefined' ? '' : value;
    }
    // ...省略
};
```

- 这里通过递归遍历保证了每个节点及子节点都会解析编译到
- 指令的声明规定是通过特定前缀的节点属性来标记，如<span v-text="content"中v-text便是指令
- 监听数据、绑定更新函数的处理是在compileUtil.bind()这个方法中，通过new Watcher()添加回调来接收数据变化的通知
- 至此，一个简单的Compile就完成了。接下来要看看Watcher这个订阅者的具体实现了

### 实现Watcher

> Watcher订阅者作为Observer和Compile之间通信的桥梁，主要做的事情是

* 在自身实例化时往属性订阅器dep里面添加自己
* 自身必须有一个update()方法
* 待属性变动dep.notice()通知时，能调用自身的update()方法，并触发Compile中绑定的回调，则功成身退。


```
function Watcher(vm, exp, cb) {
    this.cb = cb;
    this.vm = vm;
    this.exp = exp;
    // 此处为了触发属性的getter，从而在dep添加自己，结合Observer更易理解
    this.value = this.get(); 
}
Watcher.prototype = {
    update: function() {
        this.run();	// 属性值变化收到通知
    },
    run: function() {
        var value = this.get(); // 取到最新值
        var oldVal = this.value;
        if (value !== oldVal) {
            this.value = value;
            this.cb.call(this.vm, value, oldVal); // 执行Compile中绑定的回调，更新视图
        }
    },
    get: function() {
        Dep.target = this;	// 将当前订阅者指向自己
        var value = this.vm[exp];	// 触发getter，添加自己到属性订阅器中
        Dep.target = null;	// 添加完毕，重置
        return value;
    }
};
// 这里再次列出Observer和Dep，方便理解
Object.defineProperty(data, key, {
	get: function() {
		// 由于需要在闭包内添加watcher，所以可以在Dep定义一个全局target属性，暂存watcher, 添加完移除
		Dep.target && dep.addDep(Dep.target);
		return val;
	}
    // ... 省略
});
Dep.prototype = {
    notify: function() {
        this.subs.forEach(function(sub) {
            sub.update(); // 调用订阅者的update方法，通知变化
        });
    }
};
```

* 实例化Watcher的时候，调用get()方法，通过Dep.target = watcherInstance标记订阅者是当前watcher实例，强行触发属性定义的getter方法，getter方法执行的时候，就会在属性的订阅器dep添加当前watcher实例，从而在属性值有变化的时候，watcherInstance就能收到更新通知。
* 基本上vue中数据绑定相关比较核心的几个模块也是这几个，猛戳这里 , 在src 目录可找到vue源码。

> 实现MVVM


`MVVM作为数据绑定的入口，整合Observer、Compile和Watcher三者，通过Observer来监听自己的model数据变化，通过Compile来解析编译模板指令，最终利用Watcher搭起Observer和Compile之间的通信桥梁，达到数据变化 -> 视图更新；视图交互变化(input) -> 数据model变更的双向绑定效果。`

> 一个简单的MVVM构造器是这样子：


```
function MVVM(options) {
    this.$options = options;
    var data = this._data = this.$options.data;
    observe(data, this);
    this.$compile = new Compile(options.el || document.body, this)
}
```

* 但是这里有个问题，从代码中可看出监听的数据对象是options.data，每次需要更新视图，则必须通过var vm = new MVVM({data:{name: 'kindeng'}}); vm._data.name = 'dmq';这样的方式来改变数据。
* 显然不符合我们一开始的期望，我们所期望的调用方式应该是这样的：
* var vm = new MVVM({data: {name: 'kindeng'}}); vm.name = 'dmq';
* 所以这里需要给MVVM实例添加一个属性代理的方法，使访问vm的属性代理为访问vm._data的属性，改造后的代码如下


```
function MVVM(options) {
    this.$options = options;
    var data = this._data = this.$options.data, me = this;
    // 属性代理，实现 vm.xxx -> vm._data.xxx
    Object.keys(data).forEach(function(key) {
        me._proxy(key);
    });
    observe(data, this);
    this.$compile = new Compile(options.el || document.body, this)
}

MVVM.prototype = {
	_proxy: function(key) {
		var me = this;
        Object.defineProperty(me, key, {
            configurable: false,
            enumerable: true,
            get: function proxyGetter() {
                return me._data[key];
            },
            set: function proxySetter(newVal) {
                me._data[key] = newVal;
            }
        });
	}
}
```

- 这里主要还是利用了Object.defineProperty()这个方法来劫持了vm实例对象的属性的读写权，使读写vm实例的属性转成读写了vm._data的属性值，达到鱼目混珠的效果

