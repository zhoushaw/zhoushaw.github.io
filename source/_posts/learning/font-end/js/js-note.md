---
title: javascript
date: 2017-07-13 8:07:0
tags: js
categories: js
---


<div><!-- more--></div>
## javascript认识
注释:
js:1.单行注释//
	2.多行注释/**/

	css 注释 /**/
	html 注释 <!-- -->

3.javascript:运行在浏览器上的一门语言
4.javscript组成:
ECMA Script5:
BOM:浏览器对象模型
DOM:文档对象模型
javascript中大小写非常敏感

Uncaught TypeError:不可捕获的类型错误；ReferenceError:引用错误

## javascript的运行机制

0.javascript声明提前机制；
 alert(u);var u=100;alert(u);弹出结果:undefined、100；
 浏览器解析为:var u;alert(u);u=100;alert(u);
1.使用var声明所有类型的变量
2.javascript中有哪些数据类型:
a.简单类型与对象类型:
b.简单类型五种:数值类型、字符串类型、Booleans类型、Undefined类型/Null类型
c.重要:哪些类型可以转换booleans类型？所有类型都可以转换成booleans类型,有哪些类型转化成bool类型为假,哪些为真;

## 常用api

confirm("请选择");//会返回一个布尔值,确定会返回true，取消和×，会返回false
prompt("输入信息");//确定后返回输入框里面的值，没有值，确定后为空。没有值取消后为null
Math.floor()向下取整
Math.ceil()向上取整
Math.random();

## 字符类型

①.var num=0; !!num变成bool类型 
等于0或NaN:not a number;（NaN是number类型）是false;NaN不和任何类型数值相等，包括它自己。

②.var u;类型:undefined；对应布尔值false;Undefined类型中只有一个值就是undefined;

### 字符串查找

str.char At();里面输入下标，找到对象字符串里面对应位置的值

### javascript数据类型

在javscript中有七种数据类型:

> 原始类型

string、number、boolean、undefined、null(不属于Object，typeof null ==='object'为javascript历史bug)、symbol

> 复杂类型

object

> 类型判断

```
Undefined	"undefined"
Null	"object"（见下文）
Boolean	"boolean"
Number	"number"
String	"string"
Symbol （ECMAScript 6 新增）	"symbol"
宿主对象（由JS环境提供）	Implementation-dependent
函数对象（[[Call]] 在ECMA-262条款中实现了）	"function"
任何其他对象	"object"
```

```
在 JavaScript 最初的实现中，JavaScript 中的值是由一个表示类型的标签和实际数据值表示的。对象的类型标签是 0。由于 null 代表的是空指针（大多数平台下值为 0x00），因此，null的类型标签也成为了 0，typeof null就错误的返回了"object"
```

> 类型判断

```
Object.prototype.toString.call(1) // "[object Number]"

Object.prototype.toString.call('hi') // "[object String]"

Object.prototype.toString.call({a:'hi'}) // "[object Object]"

Object.prototype.toString.call([1,'a']) // "[object Array]"

Object.prototype.toString.call(true) // "[object Boolean]"

Object.prototype.toString.call(() => {}) // "[object Function]"

Object.prototype.toString.call(null) // "[object Null]"

Object.prototype.toString.call(undefined) // "[object Undefined]"

Object.prototype.toString.call(Symbol(1)) // "[object Symbol]"

```

#### instanceOf

instanceof运算符用于测试构造函数的prototype属性是否出现在对象的原型链中的任何位置

-------

分类:number、boolean、string、objcet（null，[],{}）、undefind、函数

![](https://s10.mogucdn.com/mlcdn/c45406/190129_7k9h71ch5flb581635kihdkgaific_1127x447.jpg)

#### 字符串转数字:

显示类型转换、强制类型转换
Number();
1.里面放字符串，返回成一个数字
2.如果是空字符串，或者空格，变成0
3.booleans变成对应的数字
4.如果不能转换成数字（函数，对象，不是空数字，或一个，JSON，undefind），就会返回NaN
5.空数组，null，还是0

Number是一个整体判断，如果字符串里面，有部分非数字，就会变成NaN

parseInt（）；
1.从头开始解析，一个一个的解析，如果前面是数字，保留，遇到非数字结束
2.提取前面是数字的部分
3.可以解析:+、-、空格、0。不会一开始结束
4.会转换成整数

parsefloat()
1.可以识别.在parseInt的基础上
2.还可以在后面再加一个转换的进制

#### 稀奇古怪的隐式类型转换
隐式类型转换:
1.+:
'200'-3;减、乘、除、取余可以把字符串转换成数字类型
注意:数字+字符串变成字符串；其他操作，数字跟字符串做运算，变成数字

2.-*、%:
200+'3';转换成字符串


3.++ --:
a='10'; a++、++;变成数字了

4.><:
'10'>9:比较大小
'10'>'9'字符串比较看第一位，1<9，比较的是一位一位的字符

5.！:取法，
可以转换成布尔值

6.'2'==2:表示他们最后最后进行了类型的转换,表示判断他们的值
'2'===2,先判断类型在判断值，两个只判断最终的值

7.只要没有转换成功，就会返回NaN 

#### NaN
NaN:not a number

特性:
1.NaN转换成boolean:false
2.NaN！=NaN
3.NaN是数字类型，不是数字
4.isNaN:判断是不是数字，
返回true不是数字，false是数字。

isNaN('22');首先使用Number（），将里面的字符串进行转换，如果是数字返回false


不是数字的 数字类型（一但写程序出现了NaN，就是进行了非法的运算操作），把不能转换成数字类型的数字进行了转换，所以就会出现但是又得转换，所以就出现了NaN，数字类型和数字是两种概念






### undefinnd出现的情况
什么情况下会得到undefind？
a.声明一个变量没有赋值是得到undefined;
b.函数没有显示return任何东西那么默认返回undefind
c.函数调用时，形参没有获得任何值，则return形参是undefined(最原始的undefined，在低版本浏览器中会改变undefined的值，但是这里是最原始的);
d.数组中没有显示数值的元素，默认值为undefined
e.访问一个对象不存在的属性，出现undefined

### 什么是undefind
undefined是关键字吗？答:我们可以给undefind给它赋与新的涵义。就算被赋了新的值，但是内容还是没有改变成赋给它的值，在一些比较低版本浏览器会将undefind值改变了。
我们怎样得到最原始的undefined，而无论有没有对undefind赋与新得涵义？？


③.var o=null;空类型，对应布尔值false;Null类型中只有一个值null；往往用于初始化对象类型。null和undefined:null表示已经被初始化了，而且一般用于初始化对象，undefined表示变量没有被初始化
④.var str='';空的字符串是false，不是空的字符串是true
d.||工作原理: var str=str10||'liwenqi'; 如果str10转换成bool是true，返回str10的值。否则返回后面的值

## 字符操作api
3.typeof运算符:可以返回变量的类型
typeof运算符返回结果是一个全部为小写字母的字符串:number、string、boolean、undefined、object、function
特别注意:typeof null返回的是object
typeof常用语判断一个的类型是否是函数

var num=10; alert(typeof(num))==alert(tyepof num);

## 构造函数

1.var声明变量和函数声明都在执行代码之前提前，且先提前所有var声明的变量，后提前所有函数声明，函数整个提前
```javascript
alert(typeof fun);
 var fun=100; 
function fun(){ alert(123); } 
alert(typeof fun);
==
var fun；
function fun(){ alert(123); }
alert(typeof fun);
fun=100;
alert(typeof fun);
弹出:function，number
```
2.函数
①.标准声明:（不能加分号；）
funcion fun(){}
②.表达式方式声明（匿名函数，加分号）
var fun = function(){};
③.函数可以返回任何的东西
④.
a.函数调用时实参，可以不合函数定义时形参不一致（不管是数量上，还是类型上）
b.函数内部存在一个关键字arguments用来得到，传过来的实参，arguments.length表示传过来的实参长度
c.函数的递归:
```javascript
var add=function(num1,num2){
	return num1+num2;
}//声明定义阶段
add(10,11);//调用执行阶段

var add = function(num1,num2){
	
	num1 = num1||0;
	num2 = num2||0;
	if(typeof num1=='number'&&typeof num2==
	'number')
		return num1+num2;
	else
		return NaN;

}
Math.floor();向下取整
```

## 数组操作

1.数组的length属性得到数组长度
2.通过下标访问数组中的元素
3.arguments类数组(like array)?
	可以向数组一样有length属性，还可以想数组一样使用下标来访问内部的元素，但终究不是数组，不能使用数组的方法
4.如何判断是否数组类型(不兼容低版本浏览器)
	Array.isArray(arr);返回布尔值
5.数组不存在越界错误

var arr=[];//arr.length、成员访问符
arr[arr.length]=101;//在数组的最末尾加入元素
arr.push(102);//在数组的最末尾加入元素
arr.pop();//删除末尾元素
arr.unshift(99);//在数组的头部插入元素
arr.shift();//头部删除
var n = null;
alert(typeof n);//obj

## 数组常用操作

以下方法都会修改原数组的值
Array.prototype上的方法
1.push	:尾部插入(返回数组新长度)
2.pop 	: 尾部删除(返回被删除的元素)
3.shift	: 头部删除(返回被删除的元素)
4.unshift: 头部插入(返回数组新长度)
5.splice	: 删除数组中,或在指定位置插入(返回的是删除的对象)
6.reverse: 反转数组(将做好的结果返回)
arr.reverse();
7.sort 对数组进行排序(默认是升序，
我们也可以给sort函数一个参数，而且这个参数是一个函数，
用于进行比较排序)
arr.sort(function(a,b){
		return a-b;
});升序a-b，降序b-a
var arr=[
		{name:'张三',age:15,height:167},
	 	{name:'王五',age:16,height:172},
	  	{name:'李四',age:18,height:183}
];
比较年龄:
arr.sort(function(a,b){
		return a.age - b.age;
});//从小到大排序
不会修改原数组，只有返回值是你要操作的
8.join将数组中的元素拼接成字符串，并返回，默认用',',(不会修改原数组，返回值是字符串)
可以指定符号（原数组不变）
arr.join('||');
字符串对应变成数组,不给参数默认以逗号为分割符，输入''空的，
将每一个字符分割成一个一个,空格也是字符,输入
str.split();（不会修改这个原字符串，返回值修改了）

9.slice 截取数组中的子数组（原数组不变）,
一个参数从那个参数开始到结尾，两个表示在那个区间内,
包括开头，不包括结尾那个，返回一个数组
var arr = [23,546,778];
alert(arr.slice());
arr.slice(0,-1);表示最后一个不要
window.onload = function(){
//like array
有呼吸的，动态维护，有length属性，可以通过下标访问每个元素
，
缺点:动态维护需要时间和空间成本
var lis = document.getElementById('ul').getElementsBy
TagName('li');
把like array变成Array
Array.prototype.slice.call(lis,0);
}
10.indexOf 找到目标元素在数组中的从零开始的下标位置，
如果没找到返回-1，如果第二个参数是负数，表示从后面开始数
，还是从左往右
alert(arr.indexOf('李四',2));,从下标为2的位置开始找
以下会有兼容问题，前面的都是ECMAScript5的方法
11.forEach 使用指定的方法去迭代数组中的每一个元素
对应的三个参数:
第一个参数表示，当前迭代的是值
第二个参数表示，当前迭代的是第几个
第三个参数表示，所有的数组元素
arr.forEach(function(v,i,arr){
		
});
var lis = document.getElementById('ul').getElementsBy
TagName('li');
Array.prototype.slice.call(lis,0);
lis.forEach(function(v,i){
		v.onclick = function(){
			alert(i);
		}
});
12.map 映射，将源数组按参数函数规则进行处理，
产生新的数组并返回
var result = arr.map(function(v,i,arr){
		return  v+i;//使用map时，应该显示的return的值
});
13.every检验数组中是不是每一个元素都符合函数参数验证，
函数参数应该返回的是一个boolean类型的结果
var result = arr.every(function(v,i,array){
		return v.age>=10;	
});
alert(result);
14.some检验函数中是不是存在符合函数参数验证的条件，
只要存在一个就返回真，否则假.
函数参数应该返回一个boolean类型的结果,只要有一个就可以了
	var result = arr.some(function(v,i,arr){
		return v.height>17;
	});
	
	15.filter 过滤:按参数函数规则对原数组进行过滤，
符合条件的留下，作为返回数组中的元素，否则pass，
函数参数应该返回一个boolean类型的结果
	var result = arr.filter(function(v,i,arr){
		return v>50;
	});
	16.reduce 收缩:默认从左往右，
		arr.reduce(function(a,b){
			
		});
	17.Array.isArray
 最好使用:Objet.prototype.toString.call(obj) == '[object 
Array]';	



## 对象字面量
1.对象（字面量）的本质就是:无序键值对/无序数组
2.对象可以随时随地动态开辟属性（方法）
3.所有函数内部不管你用不用都有关键字this，谁调用的函数，this就指向谁，如果没人调用函数，则函数内部的this指向全局对象window
	a.浏览器端的javascript中存在一个全局对象window
	①.this只有执行的时候才可以判断
	对象调用里面的函数，this指向的是对象
	一个构造函数直接被执行，函数里面的this
4.使用var 声明的全局变量，本质就是为全局对象window动态添加了一个对应的属性
5.全局函数中的this指向的就是全局对象window
6.①.传值和传引用

简单类型是传值

```javascript
var num=1000;
function changeValue(num){
	num =10000;
}
changeValue(num);
alert(num);
//调用changeValue时，把实参
的num值赋给形参，然后会在内存中创建一个空间
存放一个num，但在执行之后会释放空间。简单类型
的时候会将值传过去，并创一个空间
```

②.对象类型是引用(引用？别名)
```javascript
var obj = {name:'liwenqi'};
function changeValue2(obj){
	//obj.name = '张三';
	//obj = {name:'张三'};
}
changeValue2(obj);
alert(obj.name);
```

## dom操作

dom简介:
dom = docuemnt of module :文档对象模型
dom通过javascirpt 代码对页面中的内容进行增删改查(CURD)操作
CURD:CREATE UPDATE RETRIVE DELETE

1.文档节点（一个页面只有一个）document
2.元素节点（标签）
3.属性节点
4.文本节点
5.注释节点

nodeType:
1:代表元素节点

一、document.getElementById的注意事项:
1.此方法只能通过docuemnt来调用
2.找到了返回一个节点对象
3.没找到返回一个null

二、tagName:标签名属性
getElementsByTagName的注意事项:
1.此方法不但可以通过document，还可以通过元素节点对象调用，水调用就从谁的后代中去找指定的元素
2.找到了返回一个'类数组'
3.找不到也返回一个'类数组',且length属性为0
4.getElementsByTagName返回的类数组是有呼吸的，动态维护的？？就是获取了元素，赋值给了一个变量，但是这个数量会随着你增加减少元素的数量。那个变量也会跟着变化，在后面的调用过程中

console.log(aDiv.length);
var oP = document.createElement('p');
	oP.innerHTML = '这是添加p标签的内容';

var div3 = document.createElement('div');
	div3.innerHTML = '这是添加的div标签的内容';
id('div1').appendChild(oP);
id('div1').appendChild(div3);
console.log(aDiv.length);


三、document.createElement方法注意事项:
1.此方法只能通过document来调用
2.创建玩页面并不嗯呢该看到，要配合appendChild来附加到页面的指定地方


四、appendChild方法注意事项:
1.谁调用就在谁的最后一个子元素位置添加新的小儿子节点

var oP = document.createElement('p');
	oP.innerHTML = '这是添加p标签的内容';

var div3 = document.createElement('div');
	div3.innerHTML = '这是添加的div标签的内容';
id('div1').appendChild(oP);
id('div1').appendChild(div3);
console.log(aDiv.length);

五、removeChild方法的注意事项:
1.任何元素节点都可以调用此方法，谁调用就从谁的子节点去删除
2.删除目标同时，目标的所有后代都会一起删除
document.body.removeChild(id('div'));

六、改元素节点中的内容
id('div').innerHTML = '';//如果有标签解析
id('div').innerText = '';//如果有标签当文本处理

七、改特性attribute 属性property
1.	attribute:设置的是标签的特性
	property:设置的是对象的属性

增加、修改attribute的值:
id('div').setAttribute('title','liwenqi');
获取attribute的值
id('div').getAttribute('class');
id、className、value(常用特性):这三个特性可以直接获取:通过节点对象的特性直接获取
2.	行内样式
id('div').style.color ='white';
id('div').style.backgroundColor = 'red';


## javascript事件驱动
docuemnt.keyup:按下后抬起
document.keydown:按住不动
document.keypress:按下

## 正则表达式

字符串操作 
search			查找:失败返回-1，查找成功返回位置，从0开始
substring		获取子字符串，有两个参数:表示在什么区间之内，从0开始，不包括最后一位str.substring(3,5)表示获取字符串第4个到第5个的字符串
charAt			获取某个字符，输入字符串位置查找到这个位置的字符
split			分割字符串，获得数组
replace('a','b');将指定字符串的a替换成b

两种正则写法:
var re=new RegExp('/d');
var re = //d/;

任意字符
[abc]
例子:o[usb]t——obt、ost、out
范围
[a-z]、[0-9]
例子:id[0-9]——id0、id5
排除
[^a]
例子:o[^0-9]t——oat、o?t、o t

search:字符串搜索、返回出现的位置、忽略大小写:i——ignore、判断浏览器类型

match:获取匹配的项目、将匹配的相放到数组中去

量词:+、量词变化:\d、\d\d和\d+，全局匹配:g——global

replace,替换所有匹配、返回替换后的字符串
例子:敏感词过滤


组合
[a-z0-9A-Z]
实例:偷小说
过滤HTML标签
自定义innerText方法
转义字符
.（点）——任意字符
\d、\w、\s
\D、\W、\S


## javascript 原型和原型链

函数调用方式与内部this指针关系
1.直接调用:函数内部this指向全局对象window
2.通过对象使用点来调用:函数内部this指向调用对象
3.触发事件调用函数:函数内部的this指向触发事件的对象
4.以new的方式来调用:函数内部this指向本次函数执行时对应的一个匿名对象（以new的方式创建的函数，函数名的首字母一般以大写字母开始）
构造函数 ，是一种特殊的方法。主要用来在创建对象时初始化对象， 即为对象成员变量赋初始值，总与new运算符一起使用在创建对象的语句中。

5.通过call的方法来间接调用方法:函数内部this指向call方法的第一参数对象
有点:我们可以创建结构相同，但内容不同的对象


- new一个函数时，首先在内存中创造一个空对象,
- 如果这个对象是new Function创建的函数对象，那么这个对象有prototype方法，
- 创建了一个__proto__指向Object.prototype。还创建了一个constructor:
- 指向这个函数对象，创建它的目的在于，方便使用这个函数对象创建的对象，
- 使这个对象的constructor可以访问到这个创建它的函数对象。

```
var obj = new Function();

var obj = {};
obj.prototype.__proto__ = Objcet.prototype;
obj.__proto__ = Function.prototype;
obj.constructor = Function.constructor;
Function.prototype.call(obj);


var Fun = function(name){
	this.name = name;
}


Fun.prototype.__proto__ == Objcet.prototype;
Fun.constructor = Fun;

var obj = new Fun();
```

- 使用new，创建一个非函数对象的时候这个对象没有prototype方法
- 创建的__proto__指向这个创建它的构造函数的prototype
- 通过obj.constructor可以访问到这个new obj的构造函数

var obj = new Fun();
obj.__proto__ = Fun.prototype;
obj.constructor = Fun.constructor;

- 在执行这个函数，这个函数的this是指向这个对象的，
- 所以通过this给这个对象添加属性和方法，然后可以通过这个对象
- ，来访问到创建的方法和属性，每次创建一个对象都会在内存中存放一个空间，


## 跨文档传递数据

在h5新增的特性中，增加了跨文档传递信息的功能

可以在页面的位置嵌入一个iframe，向这个iframe传递数据

假设iframe的id为:iframe
则传递数据过程为:
iframe.contentWindow(内容,'*');后面一个参数指定传过去的地址（*）表示不限制地址
一般先将数据转化成JSON格式传送:JSON.stringify(msg)

接收:

```javascript
window.onmessage = function（e）{
	var msg = JSON.parse(e.data);
	//将传过来的数据转化
	e.data:表示传过来的数据
}
```


## 事件

### 事件简介

任何一个事件要经历三个阶段:
事件捕获阶段
目标对象处理阶段
事件冒泡阶段

ie6,7,8不支持事件捕获，支持冒泡

注:尽量在事件的冒泡阶段去绑定回调函数处理事件，因为捕获阶段存在兼容性问题，除非有非常特殊的需求

dom0级事件绑定	btn.onclick = function(){};
优点:兼容性好，都能绑上
缺点:只能绑冒泡阶段，不能绑多个函数，事件获取存在兼容问题


dom2级事件绑定	
优点:既可以绑捕获也可以帮冒泡阶段，可以绑多个函数
缺点:IE和非ie绑定时要使用不同的dom2事件方法；且this的涵义不一样，事件对象的获取存在兼容性

非IE6,7,8
addEventListener(默认冒泡，this指向的是调用它的对象)有三个参数:
第一个:事件、第二个:绑定的事件、第三个:是否是捕获，true捕获，false不捕获

IE6,7,8:后绑定先执行
attachEvent函数，this指向window

阻止默认行为
preventEvent


### 兼容事件
1.兼容事件获取对象
e = e || window.event;

e.type:事件类型

2.兼容阻止默认事件
id(e.preventDefault){
	e.preventDefault();
}else{
	e.returnValue = false;
}

3.兼容性的阻止事件冒泡
if(e.stopPropagation){
	e.stopPropagation();
}else{
	e.cancelBubble = true;
}

4.在冒泡事件中，
this指向的是绑定的函数
document.body.onclick = function(){//BODY
	alert(this.tagName);
}
oA.onclick = function(){//A
	alert(this.tagName);
}

兼容性获取事件源对象
if(e.target){
	alert(e.target.tagName);//非ie
}else{
	alert(e.srcElement.tagName);//ie
}
e.target = e.target?e.target||e.srcElement;

附加:了解currentTarget和immediatepropagation

5.事件的优化
删除的dom节点如果有绑定函数，对应的函数不会被删除，这样被删除的节点，所对应的函数没有清除，如果要删除这个对象，就要把对应的函数清除


### 事件清除优化

事件优化
1.清空事件
dom2级事件清除
非ie:
	document.body.addEventListener('click',fun);
	document.removeEventListener('click',fun);
ie:
	document.body.attachEvent('onclick',fun);
	document.body.detachEvent('onclick',fun);

2.事件委托（利用了事件冒泡机制）
事件委托:当你给同一个父级下面的子集添加了很多事件，可以通过父级event事件来检测到是哪个点击的，在父级里面对子集做操作，
列如:
```javascript
aA = document.getElementsByTagName('a');
for(var i=0;i<aA.length;i++){
	aA[i].onclick = function(){
		../	
	};
}
委托:

table.onclick = function(e){
	var e = e || window.event;
	var target = e.target?e.target:e.srcElement;

}
```

## 什么是闭包

简单来说可以简介为:闭包就是一个函数能够记住并访问它的词法作用域，即使这个函数在它的作用域外执行。

实例:

```
function a () {
    var s = 'sss';
    function b {
        console.log(b);
    }
}
```


