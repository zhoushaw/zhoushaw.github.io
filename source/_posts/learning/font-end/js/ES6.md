title: ES6
date: 2018-2-1 4:36:35
categories: js
tags: 
- js
- aes
---


<div><!--more--></div>

## let、const

> 总结

let命令: 用来声明一个变量，和var非常相似
const命令: 用来声明一个常量，一般用于声明数组和对象

> let特性

1.使用let声明的变量，所声明的变量只在命令所在的代码块生效
2.使用let声明的变量，不会与var一样在预解析的时候不会声明提前
3.let存在暂时性死区，在使用let声明之前无法使用声明的变量，存在暂时性死区
4.使用let无法重复声明

> const特性

const命令具有let以上的所有特性,使用const定义常量时必须注意一下几点

1.声明赋值时必须赋值
2.声明简单类型的数据不可以修改其值，声明的是数组和对象不可以修改其引用

## 解构

**基本概念:**
本质就是一种匹配模式，只要等号两边的模式相同，那么左边的变量就可以被赋予对应得值

> 结构赋值主要分为:

1.数组的解构赋值
2.对象的解构赋值
3.基本类型的解构赋值

> 数组的解构赋值(对应位置匹配)

```javascript
let [a,[[b],c]] = [1,[[2],3]];
console.log(a,b,c) //1,2,3

let [,,c] = [1,2,3];
console.log(c) // 3

let [x] = [];
console.log(c); // let x;undefined

let [y=1] = [];
console.log(y); //1 设置其默认值

```

> 对象的解构赋值(属性名赋值，真正被赋值的是变量不是属性名)

let {a,b} = {b:'111',a:'show'};
console.log(a,b);// show 111

let{a:b} = {a:1};
console.log(a,b); // undefined 1

> 基本类型的解构赋值

let [a,b,c,d] = ‘1234’
console.log(a,b,c,d);// 1 2 3 4 实际上字符变成了类数组

let {length: len} = 'hello';
console.log(len);// 5

let {tostring: ts} = 1;
let {tostring: bs} = true;
console.log(ts);
console.log(bs);

//null 和 undefined 不能进行解构赋值

## 数据结构set

集合的基本概念:集合室友一组无序且唯一(即不能重复）的相组成的。这个数据结构使用了与有限集合相同的数学概念，应用在计算机的数据结构中。
特点: key 和 value相同，没有重复的value

es6提供了数据结构set，它类似于数组，但成员的值是唯一的，没有重复的值

> 如何创建一个set

const s = new Set([1,2,3]);

> Set类的属性

console.log(s.size); //3

> Set类的方法

1.set.add(value)添加一个数据，返回set结构本身

s.add('a').add('b').add('c');
console.log(s);//{1,2,3,a,b,c}

2. set.delete(value)删除指定数据，返回一个布尔值，表示删除是否成功

console.log(s.delete('a'));// true
console.log(s);//{1,2,3,b,c}

3. set.has(value);判断该值是否有set的成员，返回一个布尔值

console.log(s.has('b'));// true

4. set.clear()清除所有数据，没有返回值

s.clear();

5. set.keys()返回键名的遍历器

console.log(s.keys());

6. set.values()返回键名的遍历器

console.log(s.values());

7. set.entries()返回键值对的遍历器

console.log(s.entries());

8. set.forEach()使用回调遍历每个成员


## 数据结构Map

**概念:**是用来存储不重复key的hash结构。不同于集合(Set)的是，字典使用的是[键,值]的形式来存储数据的.
 
Javascript的对象(object:{})只能用于字符串当做键。这给它的使用带来了很大的限制。

为了解决这个问题，es6提供了Map数据结构。它类似于对象，也是键值对的集合，但是"键"的范围不限于字符串，各种类型的值（包括对象）都可以当做键。也就是说，Object结构提供了“字符串-值”的对应，Map结构提供了"值-值"的对应，是一种更完善的Hash结构实现。如果你需要"键值对"的数据结构，Map比Object更适合

> 创建一个Map

const map = new Map([
	['a',1],
	['b',2]
]);


> Map类的属性

console.log(map.size);// map's length

> Map 类的方法

1. map.set(key,value) 设置键名key对应得键值为value，然后返回整个Map结构。如果key已经有值，则键值会被更新，否则就新生成该键。

map.set('name','zhou').set('ming','xiao');

2.map.get(key)get方法获取key对应得键值，如果找不到key，返回undefined

console.log(map.get('name'));// zhou

3.map.delete(key);删除某个健值，返回true。如果删除失败返回false

console.log(map.delete('a'));

4.map.has(key)方法回一个布尔值，表示某个键是否在当前Map对象之中

map.has('name');//true

5.map.clear()清楚所有数据，没有返回值

map.clear();

6.map.keys()返回键名的遍历器

console.log(map.keys());

7.map.values()返回健值的遍历器

console.log(map.values());

8.map.entries()返回健值对的遍历器

9.map.forEach()返回回调函数遍历每个成员

## Iterator和for...of循环

**基本概念:**

在es6中新增了Set和Map两种数据结构，再加上JS之前原有的数据结构和对象，这样就有了四种数据结构集合，平时还可以组合使用他们，定义自己的数据结构，比如数组的成员是Map，Map的成员是的对象等，这样就需要一种统一的接口机制，来处理所有不同的数据结构。

Iterator就是这样一种机制，它是一种接口，为各种不同的数据结构提供统一的访问机制，任何数据结构只需要部署Iterator接口，就可以完成遍历操作，而且这种便利操作是**依次**处理该数据结构的所有成员

Iterator遍历器的作用:
- 为各种数据结构，提供一个统一的，简便的访问接口
- 使得数据结构的成员能够按某种次序排列
- ES6新增了遍历命令for..of循环，Iterator接口主要供for...of消费


> 手写Iterator接口

```javascript
const arr = [1,2,3];

function iterator(arr){
	let index =0;
	return {
		next:function(){
			return index<arr.length?{value:arr[index++],done}:
			{value: undefined,done:true};
		}
	}
}

const it = iterator(arr);
console.log(it.next());
console.log(it.next());
console.log(it.next());


```


Iterator的遍历过程:

- 创建一个指针对象，指向当前数据结构的起始位置，也就是说遍历对象本质上，就是一个指针对象
- 第一次调用指针对象的next方法，可以将指针指向数据结构的第一个成员，
- 第二次调用指针对象的next方法，指针就指向数据结构的第二个成员。
- 不断对用指针对象的next方法，知道它指向数据结构的结束为止

每一次调用next方法，都会返回数据结构的当前成员的信息，具体来说，就是返回一个包含value和done两个属性的对象。其中，value属性是当前成员的值，done属性是一个布尔值，表示遍历是否结束

> 凡是就有Symbol.iterator属性的数据结构都具有Iterator接口

const arr [1,2,3];
const set = new Set(['a','b','c']);
const map = new Map([['b',1]]);

const itArr = arr[Symbol.iterator]();
const itSet = set[Symbol.iterator]();
const itMap = map[Symbol.iterator]();

console.log(itArr);
console.log(itSet);
console.log(itMap);

console.log(itSet.next());
console.log(itSet.next());
console.log(itSet.next());
console.log(itSet.next());

> 具备iterator接口的数据结构都可以进行如下操作

- 解构赋值
- 扩展运算符

...运算符

let str = 'zhou'
let arrStr = [...str];

console.log(arrStr);//['z','h','o','u'];

// 数组去重

const arr2 = [{},1,'a',1,'a','b',[]];
console.log([...new Set(arr2)]);


> for...of循环

const ofArr = [1,2,3,4];
for(let i of ofArr){

console.log(i);
}

const m = new Map();
m.set('a',1).set('b',2).set('c',3);

for(let [key,value] of m){
console.log(key,value);
}


## class语法

**概念:**

JS语言的传统方法是通过构造函数，定义并生成新对象，是一种基于原型的面向对象系统。这种写法跟传统的面向对象语言(比如C++和java)差异很大，很容易让接触这么语言的新手感到疑惑，所以，在es6中增加了类的概念，可以使用calss 关键词声明一个类，之后这个类来实例化对象。

> es5中基于原型的写法

const Show = function(a,b){
	this.a = a;
	this.b = b;
	return this;

}

Show.prototype = {
	constructor: Show,
	print: function(){
		console.log(this.a+‘ ’+this.b);
	}
}

const showmsg = new Show('hello','world');
showmsg.print();

> es6中class写法

class Show{
	consturucor(a,b){
		this.a = a;
		this.b = b;
		return this;
	}
	print(){
		console.log(this.a+‘ ’+this.b);
	}
}

const showmsg = new Show('hello','world');

1.Show中的constructor方法是构造方法，this关键字则代表实例对象。也就是说，es5的构造函数Show，对应es6的Show这个累的构造方法

2.Show这个类除了构造方法，还定义了一个print方法， 注意，定义"类"的方法时候，前面不需要加上function这个关键字，直接把函数定义放进去就可以了。另外，方法之间不需要用逗号分隔，加了会报错

3.构造函数的prototype属性，在es6的“类”上面继续存在:而且类的所有方法都定义在类的prototype属性上面。

4.定义在类中的方法都是不可以枚举的

5.constructor方法是类的默认方法，通过new命令生成对象实例时，自动调用该方法。一个类必须有constructor方法，如果没有显示定义，一个空的constructor方法会被默认添加

6.生成类的实例对象的写法，与es5完全一样，也是使用new 命令。如果忘记加new，象函数一样调用class，将会报错

> class的继承等相关知识

**extends** **static** **super**

1.子类继承父类使用extend关键字
2.为父类指定静态方法，使用static方法名字

super:
- 在构造函数中可以当一个函数来使用，相当于调用父类的构造函数
- 在原型方法中，可以打你个对象来使用，相当于父类的原型对象，并且会自动绑定this到子类上

## Symbol

> 什么是Symbol?

Symbol是es6中引入的类型，它是一切非字符串对象的key的集合
Symbol,表示独一无二的值，它是JS中第七种数据类型

基本数据类型:null，undefined，string，number，boolean,symbol
引用类型: Object

let s1 = Symbol();

Symbol函数前不能使用new否则会报错，原因在于Symbol是一个原始类型的值，不是对象

> Symbol参数作用

Symbol函数接收一个字符串作为参数，表示对Symbol的描述，主要是为了在控制台显示，或者转为字符串的时候，比较容易区分

> Symbol数据类型转换

console.log(string(Symbol('hello'));//Symbol(hello);
console.log(Symbol('world').toString());//Symbol(world)

console.log(!!Symbol())//true

> 作为对象属性名

let msg = Symbol('msg');

const obj = {};
obj[msg]='hello';

const data= {
	[msg]: 'hello world'
}

不能被for...in循环遍历，虽然不能被遍历，但是也不是私有属性，可以通过Object.getOwnPropertySmbols方法获得一个对象的所有Symbol属性


## 内置对象的扩展

### 字符串的扩展

> 模板字符串


let html = `
	<div>
		<span>${'首页'}</span>
	</div>`;

> repeat,includes,startsWith,endsWith


let str1 = 'a';
let str2 = str1.repeat(3);
console.log(str2);//aaa


includes,表示是否存在指定字符，返回boolean值

starsWith，endsWith。查看是否开头结尾是指定字符串，返回boolean值

### 数组的扩展

> Array.from();

var list = document.querySelectorAll('li');
var list 2 = Array.from(list);

> find,findIndex

const arr = [1,2,3,4];

arr.find((a)=>{
	return a<2;
});// 返回1


findIndex返回符合条件的第一个元素的下标

> fill()

const arr = [1,2,3,4]
arr.fill('abc',1,2);

### 对象的扩展


> 对象简写表示法

let a = 1;

const obj = {
	a
}

> 函数简写


const obj = {
	fn(){
	
	}

}

>  Object.is()


console.log(Object.is(NaN,NaN));//false
console.log(Object.is(+0,-0));//false

> Object.assign()

用于对象的合并，将源对象的所有可枚举属性，赋值到目标对象


let obj1 = {a:1};
let obj2 = {a:2,b:3}
let obj3 = {c: 'abc'};

Object.assign(obj1,obj2,obj3);
console.log(obj1);//{a:2,b:3,c:'abc'};

### 函数的扩展

> 为函数指定默认值

function fn(a=10,b=20){

	return a+b;
}

> reset参数

rest 参数形式为("...变量名")，用于获取函数的多余参数，这样就不需要使用arguments对象了，rest参数搭配的变量是一个数组，该变量将多余的参数放入数组中

**rest参数后不能再增加参数**
function sum(...arr){
	var count = 0;
	for(let i =0;i<arr.length;i++){
		count+= arr[i];
	}
}

> 使用箭头函数

const fn = a=>a;//如果是一行时，默认返回第一行的内容

const fn = (a,b)=>({a:0,b:1});返回对象时要使用()包裹


1.箭头函数体内没有自己的this对象，所以在使用的时候，其内部的this就是定义时所在环境的对象，而不是使用时所在环境的对象

```javascript
function fn(){

	setTimeout(function(){
		console.log(this);
	})

	setTimeout(()=>{
		console.log(this);
	});
}

var obj = {a:1};

fn.call(obj);// windows,Object{a:1}

```

2.不能给箭头函数使用call apply bind去改变其内部的this指向


3.箭头函数体内没有arguments对象，如果要用，可以用Rest参数代替

4.不可以当做构造函数，不可以使用new命令，否则会抛出一个错误

5.箭头函数不可以当做Generator函数


## Promise

**基本概念**
Promise: 是es6中新增的异步变成解决方案，提现在代码中它是一个对象，可以通过Promise构造函数来实例化

new Promise(cb) ===> 实例的基本使用Pending Resolved Rejected

> 两个原型方法

- Promise.prototyp.then()
- Promise.prototype.catch()

> 两个常用的静态方法

- Promise.all()
- Promise.resolve();


new Promise(cb)
//Pending(进行中)===> Resolved(已完成)
//Peding(进行中)===> Rejected(已失效)

```javascript
const imgs = [
	'http://image1.com/image1.jgp',
	'http://image1.com/image2.jgp',
	'http://image1.com/image3.jgp',
]
function loadImg(url){

const p = new Promise(function(resolve,reject){

	const img= new Image();
	img.src = url;
	img.onload = function(){
		resolve(this);
	};
	
	img.onerror = function(err){
		reject(err);
	}
});
return p;
}

p.then(function(image){
	document.body.appendChild(image);
})

```

> Promise.all

**概念:**
Promise.all可以将多个Promise实例包装成一个新的Promise实例

- 当所有Promise实例的状态都变成了resolved，Promise.all的状态才会变成resolved，此时返回值组成一个数组，传递给then中的resolve函数
- 只要其中一个被rejected.Promise.all的状态就变成了rejected，此时第一个被reject的实例的返回值，会传递给p的回调函数

const allDone = Promise.all([loadImg[imgs[0],loadImg[imgs[1],loadImg[imgs[2],loadImg[imgs[3]])

allDone.then((datas)=>{

	datas.forEach((item,i)=>{
		document.body.appendChild(item);
	});
});


> Promise.resolve()

//参数是Promise实例，将不做任何修改，原封不动返回这个实例
Promise.resolve(loadImg(imgs[0])).then(function(img){
	document.body.addpendChild(img);
});


// 将对象转成promise对象，然后就立即执行thenable对象的then方法
Promise.resolve({
	then(resolve,reject){
		const img = new Image();
		img.src= imgs[1];
		img.onload = function(){
			resolve(this);
		}
	}
}).then(function(img){
	document.body.appendChild(img);
});

Promise.resolve('miaov');






