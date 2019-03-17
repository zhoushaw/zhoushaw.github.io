---
title: http
date: 2018-09-30 8:07:12
tags: http
categories: learning
---


## 同源策略

在了解跨域问题前，先对同源策略进行一个回顾

> 同源策略

* 同源策略是网景公司提出的著名的安全策略
* 现代浏览器构建都基于同源策略
* web构建在同源策略基础之上，对非同源的脚本限制就是同源策略的实现
* 同源指的是，协议、域名、端口三者相同称之为同源，任一不相同，则不同源

<div><!-- more--></div>

> 同源策略的限制规则

* DOM层面
    * 限制了不同域的docuemnt对象，或js脚本禁止对当前域的document对象或属性进行修改
* Cookie(localstorage和IndeIndexDB也包含)    
    * 不同源之前的cookie无法进行读取
    
* 非绝对性
    * 同源策略通常允许嵌入外部资源，列如在网页中使用video、script、img嵌入外部资源，同源策略关注的是，页面加载js所在的域，而不是页面存放js所在的域。通常不允许读操作，例如嵌入iframe读取不同源的文档内容。
    * h5提供了postMessage可以解决不同域消息通知问题，可自行百度这里就不详细赘述
    
> 关于同源策略相关的问题

* 没有同源策略会怎样，为什么同源策略禁止读操作
    * 设想你打开了一个银行网站a，这是一个钓鱼网站，这个钓鱼网站通过iframe嵌入了工商银行网站，用户进入钓鱼网站后，在没有同源策略限制的情况下会发生什么呢？
    * 银行页的DOM元素将被修改
    * 银行卡页面的DOM属性将被修改
    * 钓鱼网站将会获取用户cookie，支付密码等信息，可以伪造用户请求，发起转帐等操作
* 有了同源策略会怎样
    * 页面在执行js脚本前，先确定当前执行脚本是不是当前域的，若不是当前域，则禁止js脚本执行
    * 注意浏览器不关心你的js脚本是不是从当前域加载过来的，浏览器只关心执行js的页面是不是和当前页面同源
    
> 为什么`<script><video><img><audio>`等带src标签可以不遵守，同源策略。可以跨域嵌入

* 若大型网站，每个资源都必须同源，那所有资源都必须放在同一台服务器上。网站的构建将会受到一定的限制
* 同时页面内容引入的外部资源，将会由网站开发人员定义引入，网站开发人员会确定引入资源的安全性
* 网站a.com可以通过`<script src="www.baidu.com/b.js"></script>`，a网站引入了b网站的脚本，这完全是可以的，不受任何限制，可以这样认为，这要当前页面引入的资源都认为，这个资源和当前页面同源，而不关心这个资源具体从哪个资源引入


> 对于跨域资访问说明

* 不同浏览器的跨域访问限制条件并不一定一致，有的允许跨域访问indexDB、有的不允许跨域写操作
* 其他跨域访问机制:CORS允许一个域向另一个域发送AJAX请求、OAuth(跨域授权)
* 严格的同源策略，限制所有非源资源的读写，非源资源的嵌入。这样开发者必须将所有资源放至同一台服务器上，这样不免限制了灵活性和扩展性
* 现在的同源策略，对方便和安全之前作出了权衡，既保证了安全性，也提升了方便性

## 跨域方法

`前面已经大概讲了同源策略的相关概念`


> 几种跨域访问策略

* document.domain设置
    * 可通过document.domain进行设置不同域名共享cookie,设置`document.domain=demo.com;`这样a1.demo.com和a2.demo.com就可以共享cookie(这种方法只适用于cookie和iframe)
* JSONP
    * 是开发者通过对同源策略的了解，开发的一种非官方的跨域数据交互协议
    * 利用了`<script><audio><img>`的src属性天生支持跨域的属性开发的
    * 开发者利用js动态创建script标签，script的src请求的地址是服务端地址接口地址，并且在请求地址后约定返回客户端的函数名称，客户端首先定义好接收服务端参数的函数，发送至服务端，服务端返回一个自执行函数，函数的参数是服务端返回的值，函数是客户端定义好的
* postMessage方法
    * postMessage是h5新定义的，支持跨域资源访问的方式

> CORS请求

**CORS**是W3C的一个标准，全称局域资源共享
`它允许浏览器向不同源域发送XMLHttpRequest请求，从而克服了AJAX只能向同源域名发出AJAX的限制`

> 使用CORS需要浏览器和服务端同时支持，浏览器版本必须大于IE10，浏览器端若是支持，会自动完成浏览器端的操作。因此使用CORS关键是服务端，支持CORS跨域请求

* 跨域资源请求分为**简单请求**和**非简单请求**
* 简单请求(同时满足以下条件)
    * 请求方式是下面三种之一:1.HEAD 2.POST 3.GET
    * HEAD参数不超出:
        * Content-Type:只限于三个值
            * application/x-www-form-urlencoded、
            * multipart/form-data、text/plain、
            * Accept
        * Accept-Language
        * Content-Language
        * Last-Event-ID

    * 对于简单请求，浏览器会在request的Header中添加origin: 当前url，当上请求源地址
        * 如果请求源不在服务端请求源白名单内，服务端不会返回Access-Control-Allow-Origin，XMLHttpRequest会报出错误异常
        * 如果origin在服务端白名单内，会返回
            * Access-Control-Allow-Origin: http://api.bob.com
            * Access-Control-Allow-Credentials: true
            * Access-Control-Expose-Headers: FooBar
* 非简单请求
    * 对于非简单请求，浏览器在进行交互前会发送options方法，进行预检测
    * 服务端会对:`Origin、Access-Control-Request-Method和Access-Control-Request-Header`字段进行检测，若检测通过，会发出正常的XMLHttpRequest请求

> Access-Control-Allow-Credentials: true

用来决定，进行CORS共享是，是否发送cookie

**CORS跨域请求比JSONP请求方法更多，传输内容类型更多，但兼容性没有JSONP强**

