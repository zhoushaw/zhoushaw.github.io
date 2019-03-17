title: 知识大杂烩
date: 2018-02-01 6:52:35
categories: js
tags: js
---

<div><!--more--></div>
## SEO

1.合理的title、description、keywords:搜索引擎对于三项的权重逐个减小。
2.使用语义化标签，爬虫更容易理解和抓取
3.重要内容不要使用js外部引入，爬虫不容易抓取
4.网页加载速度也是爬虫评判的重要标准
5.每个页要只能出现一次H1标签，H2~H6标签可以多次，这样做是为了加重H1标签的权重。 


## XMLHttp 原生写法


```javascript
	let xhr = null

	try{
		xhr = new XMLHttpRequest();
	}catch{
		xhr = new ActiveXObject('Microsoft.XMLHttp');
	}

	xhr.open('get','www.baidu.com',true);
	xhr.send();

	xhr.onreadystatechange = function(){
		if(xhr.readyState==4&&xhr.status==200){
			alert(xhr.responseText)
		}
	}
	
```

## 数组

> 修改原数组

push
pop
shift
unshift
reverse
splice


> 不修改原数组，返回处理的新数组

slice
sort

## cookie、sessionStorage、localStorage

> 区别

- 大小:

    cookie  -- 5kb
    sessionStorage  -- 5MB
    localStorage    -- 5MB
    
- 使用场景:

    cookie  --  服务端在请求头报文中增加set-cookie，请求回来时自动将cookie存入本地。在同源http请求中将自动在request Head中携带cookie
    
    sessionStorage -- 通常可以配合cookie使用，列如当用户登录淘宝后，访问的每个页面都需要保持持续登录，服务器会创建好session，
    并关联的session_id通过set-cookie添加到响应头中，浏览器接收到cookie后会将其存入指定位置，当发送同源的http请求时可以自动发送cookie
    
    localStorage  -- 可以存储用户数据，可以用来存储token、userId内容，当登录成功后将获取到的token存入localStorage中，
    每个http请求头中添加token，这样也获得了持续验证

- 存储时间:
    
    cookie -- 设置失效时间，到达失效时间后对应的cookie将消失
    
    sessionStorage  -- 当对应的页面，标签或浏览器关闭后，sessionStorage将失效
    
    localStorage -- 永久保存，只有同源域名下才可以访问到对应的localStorage

## iframe特点

> 优点

更加快速构成网页结构，编写导航更加便捷

> 缺点

1.多个框架构成的网页代码变得更加复杂，不容易管理从而带来不好的用户体验
2.网络爬虫，读取到iframe时，找不到链接，认为该网站是死网站，放弃爬取该网站内容
3.网站前进后退按钮只对光标所在的页面生效
4.使用iframe会阻塞js的onload进程
5.iframe中的css和js必须外链引入增加http请求，降低性能

## web标准和w3c标准

> web标准

web标准是由多个标准组成的: 结构化标准，表现标准，行为标准
对应标准也分为: 
    1.结构化标准指XML和XHTML
    2.表现标准是指css
    3.行为标准w3c DOM和 ECMAScript
    
> w3c标准

web标准中的大部分标准都是万维网联盟制定的，但也有些标准是其他组织进行制定的列如ECMAScript


## XHTML和HTML

XML: 可扩展标记语言
HTML: 超文本链接
XHTML: 可扩展的超文本链接

> HTML

网页内容标记语言，是一个标准，是网页构成的基本内容。
超文本的内容除了文本，还可以表示图片，音频，视频等内容。
它的作用是一个规范，告诉所有浏览器统一标准

> XML

XML的表现形式上来说就是给文档加一堆标签，告诉文档对应部分的内容是什么。
这样做的目的是方便数据存储，传输，分享数据。也更加方便人和机器阅读
XML和HTML的区别是，HTML:是预定义的，再使用前就定义好了，不能凭空造一个新标签然后使用
而XML则不同，可以自己发明标签，也就是可扩展的意思

> XHTML 

```javascript
XHTML实际上就是HTML和XML的混合体，出现的原因是因为，HTML是一种语法比较松散的标记语言，语法要求也不严格。
比如:不区分大小写，单引号和双引号都可以，属性值加不加引号都可以，所谓没有规矩不成方圆
XHTML1.0是基于HTML1.0的，它没有引入任何新的标签和属性，XHTML 是更严格的HTML，它相当于HTML的子集.几乎所有能正确解析HTML的浏览器，都能兼容XHTML
XML设计用来传送及携带数据信息，不用来表现或展示数据
标签必须使用 />实现闭合例如<br />而不能使用<br>  
```

## Doctype作用? 严格模式与混杂模式如何区分？它们有何意义?

> Doctype

位于html标签前面，用来声明使用XML或XHTML规范

> 严格模式

所谓的严格模式是以浏览器支持的最高的w3c标准解析执行代码；

> 混杂模式

在混杂模式中，页面以宽松的向后兼容的方式显示。模拟老式浏览器的行为以防止站点无法工作。

> 何时出现对应模式

浏览器使用严格模式还是混杂模式取决于，
html中的DTD(文档类型声明),文档中定义了标准的DTD声明，则会使网页使用对应的方法标准解析加载网页
忽略了文档中的DTD声明，则会采用

## 行内元素有哪些？块级元素有哪些？ 空(void)元素有那些？行内元素和块级元素有什么区别？

> 行内元素

b,img,font,textarea,input,label,button,select,em,i,span,

> 块元素

div,p,section,header,table,tbody,tfoot,h1-h6,iframe,option,ul,li,ol,dl，address,tr,hr,br

## 闭包

> 什么是闭包

闭包其实就是可以读取其他函数变量的函数，这种引用的产生导致，变量将常驻内存导致无法释放

> 如何使用闭包

编写一个函数a，函数a里面有一个函数b，函数b里面引用了函数a内的变量

> 闭包带来的优点和缺点

在javascript中并没有私有变量这个概念，可以通过闭包来实现私有变量和私有方法，减少全局污染
使用闭包会造成变量常驻内存，使用不当容易造成内存泄漏，解决方法在函数退出前，将不适用的局部变量删除

## 作用域链

> 什么是作用域链

作用域链是执行环境中函数和变量的可访问性是有序的，变量的访问权限是一直向上查找的，一直查找到windows停止。作用域向下访问时不允许的
简单的说作用域链就是函数和变量的可访问范围，即作用域链控制着函数和变量的生命周期和可访问性

## 原型链

> 前言

javascript中函数也是一个对象

> 原型链prototype

javascript中的函数可以当做构造函数使用，约定构造函数的首字母大写，使用new生成一个实例对象
每个函数再生成时都会附带一些原有属性，每个函数都有一个prototype属性指向这个函数的原型，原型里面自带__proto__属性和constructor
另外原型里面可以定义方法，在生成的实例对象中可以使用prototype定义的方法，生成的实例对象在调用方法时，首先会在自身上查找是否有该方法，
没有方法时会到构造函数的原型上查找，没有查找到通过__proto__向更上层的原型对象查找是否有该方法，直至找到Function.prototype。

如果需要实现继承，将要继承的函数的原型的proto等于继承函数的实例，因为继承函数的实例里面有__proto__可以查找到继承函数的原型，就可以使用继承函数的方法和变量了

生成的实例对象中含有__proto__这个属性，proto属性指向生成这个构造函数的原型，通过constructor可以找到这个实例对象的构造函数

而通过这个构造函数生成的实例对象会生成一个__proto__属性，这个属性指向它构造函数的prototype


## 有赞

> 为什么要离开现在公司

公司的技术氛围不是很好，在公司发展受限

> 常见算法时间复杂度，排序算法的时间复杂度

O(n^2)

> position 有哪些属性，定位时根据什么进行定位

属性:
    static
    relative
    absolute
    fixed

设置了static后，left和top不起作用
设置relative，left和top的偏移将会以自身当前位置做偏移
absolute，一直向上查询找到设置了属性为relative，absolute，fixed的父元素
fixed以窗口为基准进行偏移

> 如何解决微信定位不准的问题

使用wx.getLocation获取到当前经纬度，使用wx.request向腾讯的地图接口发送请求获取当前地址信息


> http三次握手

白话翻译:
client-> server 我要发送http请求了
server-client 可以你发吧
client-> server 好，那我发送了

> js数据类型，及如何判断

数据类型:
    boolean，object，string，null，undefined，number，symbol

typeof boolean  > boolean
typeof object   > object
typeof array    > object
typeof function > functioin
typeof null     > object
typeof number   > number
typeof undefined > undefined

判断一个是否为对象时

```javascript
    function isObject(item){
        let type = typeof item;
        return type ==='object'||type==='function'&&item!==null;
    }
    
```

> 判断其是否是dom对象

dom.nodeType ===1,是dom对象


> 小程序如何实现分享

在js文件中定义onshareAppmessage，可以设置图片路径，标题，打开的页面路径
不设置图片和标题使用，图片使用当前页面截图，标题使用当前页面标题，或者首页标题，


## HTTP

> 常用的http方法

get,post,head,put,delete,options,trace,connect，link


get获取远程资源
post传输实体
head获取请求头
put获取文件
delete删除远程服务器文件
connect与与远程服务器保持连接
options检测远程服务器是否支持指定类型的方法

> get与post文件区别

浏览器会主动缓存get的请求，
get相对于post而言，post更加安全，因为get已明文的方式显示在地址栏上，而post放在request body中，抓包情况下一样
post使用request body进行传输，所以支持更多的数据传输长度，并且支持更多种数据类型，而浏览器的url长度有限

> http状态

http是无状态的，不存储状态，使用http1.1开始自动建立持续连接

## html5新特性

> 新增标签:

语义化标签:
article，section，aside，header，footer

新特性标签:
video，canvas，audio，css3新动画特效

> 去除的标签:

basefont,u,tt,s,font

> css3特性

1.选择器的扩展，属性选择器，后代选择器
2.边框，背景
3.渐变，阴影
4.盒模型

> 标准盒模型，怪异盒模型

标准盒模型的块宽度等于padding+margin+border+width
怪异盒模型的块宽度等于margin+width

## 闭包

闭包是什么？为什么产生闭包？闭包的作用？

> 什么是闭包

在了解闭包之前我们先来讲解一下作用域链，假设我们声明了一个函数b，b函数中包含一个函数a，而a函数中console.log(s);如果当前作用域没有s变量，则会向上一个作用域寻找s变量.假设函数b中有声明变量s，这个时候就形成了闭包
当我们在函数b中声明了变量s，并且return了函数a，这个时候函数a形成了闭包


> 为什么会产生闭包

根据垃圾回收机制，如果一个变量的引用不为0，那么这个变量就不会被释放，当这个变量一直不会释放就会一直存储在内存中，从而形成了我们所知的闭包。当将函数内部的函数返回出来，并且将返回的函数存入一个全局变量，那么这个全局变量不会被释放，所有内部的变量也不会被释放，变量将会一直保存在变量中

> 闭包的作用

在javascript中可以直接读取全局的变量，但是一个函数中不可以读取其他函数的变量。而闭包正好实现了一个变量读取其他函数的变量，闭包形成私有变量，减少全局变量的污染

## 预加载

> preload的作用

1.不阻塞渲染和document的onload事件
2.提前加载指定资源，不会出现字体半天才出现的情况

```javascript
<link rel="preload" href="style.css" as="style">
<link rel="preload" href="main.js" as="script">
```




## http缓存

### http缓存的介绍
> 为什么有http缓存，什么时候出现作用是什么

http缓存也可以理解成客户端缓存，相当于客户端有个本地数据库，可以用于存储图片，js，这些常见的静态文件，分成强制缓存和协商缓存

> 强制缓存

当设置http请求头中设置了缓存类型为强制缓存时，会将资源缓存入本地，当再次发送请求获取这些资源的时候，会直接读取缓存在本地的这些数据，当本地数据库没有这些文件的时候才会从服务端读取

> 协商缓存

协商缓存又可以称之为对比缓存，客户端会首先从缓存数据库获取一个标识，得到标识后向服务端验证缓存的资源是否新鲜，如果该资源还是新鲜的资源，服务端会返回304，这时客户端会从本地读取缓存数据

> 浏览器是如何判断本地缓存资源是否新鲜

在客户端与服务端进行交互的时候会发送http请求，http请求是由请求头和请求体构成，在请求头中有cache-control中附带缓存信息，时间等数据信息，客户端可以根据这个来判断是否是新鲜数据

### 如何使用缓存技术

> 如何使用强制缓存

对于强制缓存服务端会使用两个字段来表明，expires和cache-control

expires:

expires的值为服务端返回的数据到期时间，当再次请求时的请求时间小于expires的时间，客户端则直接使用缓存的数据，但由于服务端和客户端的时间可能有时间差，所以一般使用cache-control代替

cache-control:

cache-control有很多属性分别表示不同的缓存策略

private:	客户端可以缓存
public:		客户端和服务端都可以缓存
max-age=t	表明资源会在多少秒之后失效
no-cache:	表明使用协商缓存
no-store:	不使用缓存

> 协商缓存

协商缓存需要对比是否使用缓存，在客户端第一次向服务端发起请求的时候，服务端会向客户端发送缓存标识和缓存数据，客户端会将缓存数据存入本地，再次请求时客户端会将缓存标识发给服务端，当服务端会验证这个标识是否新鲜，当该资源新鲜时直接返回，304状态这时客户端会直接使用缓存文件，当资源不够新鲜时，服务端会直接发送最新的数据过来

Last-ModifiedLast-Modified:服务器在响应请求时，会告诉浏览器资源的最后修改时间。
if-Modified-Since:浏览器再次请求服务器的时候，请求头会包含此字段，后面跟着在缓存中获得的最后修改时间。服务端收到此请求头发现有if-Modified-Since，则与被请求资源的最后修改时间进行对比，如果一致则返回304和响应报文头，浏览器只需要从缓存中获取信息即可。从字面上看，就是说:从某个时间节点算起，是否文件被修改了

如果真的被修改:那么开始传输响应一个整体，服务器返回:200 OK
如果没有被修改:那么只需传输响应header，服务器返回:304 Not Modified

if-Unmodified-Since:从字面上看, 就是说: 从某个时间点算起, 是否文件没有被修改

如果没有被修改:则开始`继续'传送文件: 服务器返回: 200 OK
如果文件被修改:则不传输,服务器返回: 412 Precondition failed (预处理错误)

这两个的区别是一个是修改了才下载一个是没修改才下载。Last-Modified 说好却也不是特别好，因为如果在服务器上，一个资源被修改了，但其实际内容根本没发生改变，会因为Last-Modified时间匹配不上而返回了整个实体给客户端（即使客户端缓存里有个一模一样的资源）。为了解决这个问题，HTTP1.1推出了Etag。

### 如何禁止浏览器缓存input框的输入内容

input框有autocomplete属性，有on和off值，默认为on，设置为off即可

### input框的属性

> 所有方法有

image,radio,hidden,checkbox,password,reset,submit,text,button

### 数组中有哪些方法

> 会修改原数组的方法

splice,sort,push,pop,shift,unshift,reverse,

> 不会修改原数组的方法

forEach,filter,some,every,map,reduce,join,slice,indexOf

> 数组中的如何中断

数组中的方法都不可以中断，return也无效。只有some和every为return false的时候会中断


### 如何检测css动画如何终止

> 通过事件监听transitionend，是否执行来判断是否执行结束

el.addEventListener('transitionend',function(){
    console.log('css动画结束')
    // todo
})

### vue-router如何实现的

前端路由是直接找到与地址匹配的一个组件或对象并将其渲染出来。改变浏览器地址而不向服务器发出请求有两种方式: 
1. 在地址中加入#以欺骗浏览器，地址的改变是由于正在进行页内导航 
2. 使用H5的window.history功能，使用URL的Hash来模拟一个完整的URL。

当打包构建应用时，Javascript 包会变得非常大，影响页面加载。如果我们能把不同路由对应的组件分割成不同的代码块，然后当路由被访问的时候才加载对应组件，这样就更加高效了。

### http的常见方法

> 前面已经描述


### 正则表达式空格怎么表示

> 特殊字符

^,$,.,*,+,{},[]

> 正则修饰

i: 不区分大小写
g: 全局匹配

> 量词

.:一个或零个
+:一个或多个
*:零个或多个
{1,}一个或多个
{1,6}一个到六个

>字符类

\w:匹配单词字符，包括字母数字下划线
\s:匹配空格
\d:匹配数字
\t:匹配制表符
\r:匹配回车符
\n:匹配换行符

字符类大写后，表示相反

> 字符串上的方法

match:将匹配的内容当做数组返回，没有则返回null
replace: 接收两个参数，第一个正则，第二个替换成的内容，将匹配到的内容全部替换
search: 如果找到对应内容返回索引，否则返回-1


> 正则上的方法

test: 如何匹配到了返回true否则返回false
exec: 将第一次匹配到的内容和子匹配到的内容放入数组中


### cookie的操作，如何设置cookie的目录

> 读取cookie

document.cookie可以获取到cookie的值

> 读取不太友好，需要自己封装，可以配合正则使用

get: function (name){ 
        var cookieName = encodeURIComponent(name) + "=", 
            cookieStart = document.cookie.indexOf(cookieName), 
            cookieValue = null; 
        if (cookieStart > -1){ 
            var cookieEnd = document.cookie.indexOf(";", cookieStart); 
            if (cookieEnd == -1){ 
                cookieEnd = document.cookie.length; 
            } 
            cookieValue = decodeURIComponent(document.cookie.substring(cookieStart + cookieName.length, cookieEnd)); 
    } 
        return cookieValue; 
}

> 写入

set: function (name, value, expires, path, domain, secure) { 
    var cookieText = encodeURIComponent(name) + "=" + 
                        encodeURIComponent(value); 
    if (expires instanceof Date) { 
        cookieText += "; expires=" + expires.toGMTString(); 
    } 
    if (path) { 
        cookieText += "; path=" + path; 
    }   
    if (domain) { 
        cookieText += "; domain=" + domain; 
    } 
    if (secure) { 
        cookieText += "; secure"; 
    } 
    document.cookie = cookieText; 
}

> 删除cookie

unset: function (name, path, domain, secure){ 
    this.set(name, "", new Date(0), path, domain, secure); 
}

> cookie安全

HttpOnly=true   // 只能在发送http时携带，无法通过js读取到cookie
cookie被设置了Secure=true，那么这个cookie只能用https协议发送给服务器，用http协议是不发送的


### svg有用过吗，canvas如何使用

svg创建的是矢量图，使用xml构建，xml扩展描述语言出现比较早，内置rect，circle，line，等标签主要用于描述二维。每个图形都是dom节点可以绑定事件或用于修改
canvas画布，输出的是整个画布，就像一张图片一样放大会出现锯齿

### vue的双向绑定原理是怎么样的

数据劫持(observer)=>订阅者(watcher)=>指令模板(complite)

### 你是怎么学习的

前期会看一下视频，后期主要是通过mdn系统学习api，在知乎掘金等社区发现好玩高效的特性，看源码

### transition有哪些属性，可以设置什么。同理去学习一下animation

> transition

transition: property duration timing-function delay;

> transform

transform: none|transform-functions;
none | matrix(n,n,n,n,n,n) | translate(x,y) | translate3d(x,y,z) | translateX(x) | translateY(y)

### 常见的网络安全问题，如何解决sql注入，xss攻击，CSRF的防御

> sql 

在提交表单时，里面输入sql语句，如果服务器端是使用sql拼接方式。则数据库可能遭到恶意修改

> xss

将html标签或javascript注入到网页中，可以获取到用户的cookie，获增加恶意表单，用户提交时会将信息发送到攻击者的服务器上

在用户输入的地方要检测<>之类的标签

> csrf

跨站伪造请求，原理很简单，假设我在论坛上发布了一篇文章，文章有一张图片，scr="http://www.cnblogs.com/mvc/Follow/FollowBlogger.aspx?blogUserGuid=4e8c33d0-77fe-df11-ac81-842b2b196315",当你打开这篇文章的时候，src为自动发送http请求，并携带你的token。

我在我的文章中放了一个连接指向我的一个网站，我在网站内嵌入了iframe，在网页加载的时候我就使用iframe发送http请求，这个时候你的token就会自动添加到http中并进行发送，但由于同源策略这样是加载不出来的，新建一个页面用户存放iframe，当前页面src嵌入iframe



### promise状态有哪些，有哪些方法。所有promise执行完了之后有个finally方法

> 状态
peding

### vue的生命周期有哪些，分别做了什么

### h5的离线存储

### 如何防止使用js在浏览器中获取到cookie

设置httpOnly=true,document.cookie = ""

### jsonp的跨域原理

### input如何禁止浏览器缓存用户的登录信息

autocomplete = false

### es6中如何实现双向绑定
proxy代理实现，与Object.definedProperty不同，可以检测数组变化
### 箭头函数和普通函数有什么区别

1.箭头函数作为匿名函数,是不能作为构造函数的,不能使用new
2.箭头函数不绑定arguments,取而代之用rest参数…解决
3.箭头函数会捕获其所在上下文的 this 值，作为自己的 this 值
4.箭头函数当方法使用的时候没有定义this绑定
5.箭头函数没有原型属性
6.箭头函数不能当做Generator函数,不能使用yield关键字
7.箭头函数不能换行
8.箭头函数的this永远指向其上下文的 this，任何方法都改变不了其指向，如call(), bind(), apply()
普通函数的this指向调用它的那个对象

### 事件委托是如何实现的

在事件冒泡阶段，将事件代理到父元素上，通过currentTarget和target来查看触发元素的关系，通过这种方式来减少js，提高性能

### 移动端的点击穿透是为什么
一般出现这种状况是click和touch事件混用出现的，因为click默认有200毫秒的延迟，而toucch事件没有延迟在弹窗消失后依然会触发click事件，导致底层元素点击事件触发

### box-sizing有哪些属性，那些元素是默认border-box的
content-box，可以通过这个元素将其设置成标准盒模型，和怪异盒模型

### background-clip属性和background-origin属性

background-clip是用于设置，背景图从什么位置开始显示的，border-box、content-box、padding-box
background-origin指定background-position以什么位置作为标点进行定位

### 网页中使用什么类型的图片该如何取舍

### 如何设置input框中占位信息的样式
input:[placehodler]{}
进行设置样式

### 如何设置像五角星一样的不规则点击区域
通过svg的polygon属性进行设置

### scss有些什么功能，extend

extend可以进行继承，
可以进行变量定义，可以for循环
 mixins进行函数式编写css
 


