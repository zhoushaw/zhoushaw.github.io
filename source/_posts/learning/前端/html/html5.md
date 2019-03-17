---
title: html5
date: 2017-07-9 7:11:00
tags: html5
categories: html
---


<div><!-- more--></div>

## 常用语义标签

### 无功能标签:
<header></header> 页眉，主要用于页面的头部的信息介绍，也可用于板块头部

<hgroup></hgroup> 页面上的一个标题组合，一个标题和一个子标题，或者标语的组合
<hgroup>
	<h1>妙味课堂</h1>
	<h2>带您进入富有人情味的IT培训</h2>
</hgroup>

<nav></nav> 导航 （包含链接的的一个列表）
<nav><a href=“#”>链接</a><a href=“#”>链接</a></nav>

<footer></footer>页脚  页面的底部 或者 版块底部
<section> <section> 页面上的版块
用于划分页面上的不同区域,或者划分文章里不同的节
<article></ article > 用来在页面中表示一套结构完整且独立的内容部分
可以用来呈现论坛的一个帖子，杂志或报纸中的一篇文章，一篇博客，用户提交的评论内容，可互动的页面模块挂件等。



<aside></ aside> 元素标签可以包含与当前页面或主要内容相关的引用、侧边栏、广告、nav元素组，以及其他类似的有别与主要内容的部分
aside 的内容应该与 article 的内容相关。
被包含在<article>中作为主要内容的附属信息部分，其中的内容 以是与当前文章有关的引用、词汇列表等
在<article>之外使用，作为页面或站点全局的附属信息部分；最典型的形式是侧边栏(sidebar)，其中的内容可以是友情链接、附属导航或广告单元等。


<figure> < figure > 用于对元素进行组合。一般用于图片或视频
 <figcaption> <figcaption> figure的子元素 用于对figure的内容 进行说明
	<figure>
		<img src=“miaov.png”/>(注意没有alt)
		 <figcaption> 妙味课堂 photo &copy 妙味趣学</figcaption>
 </figure>

<time></time>用来表现时间或日期

<address></address> 定义文章 或页面作者的详细联系信息

<mark></mark> 需要标记的词或句子


<dialog></dialog>定义一段对话
<dialog>
  <dt>老师</dt>
  <dd>2+2 等于？</dd>
  <dt>学生</dt>
  <dd>4</dd>
  <dt>老师</dt>
  <dd>答对了！</dd>
</dialog>




### 有功能的标签:

<datalist></datalist>选项列表。与 input 元素配合使用，来定义 input 可能的值。
<input type="text" list="valList" />
    <datalist id="valList">
	     <option value="javascript">javascript</option>
	     <option value="html">html</option>
	     <option value="css">css</option>
    </datalist>

<details></details>用于描述文档或文档某个部分的细节
该元素用于摘录引用等 应该与页面的主要内容区分开的其他内容
Open 属性默认展开
< summary></summary> details 元素的标题



<progress><progress>定义进度条
<progress max="100" value="20">
         <span>76</span>%
</progress>


## 表单

email  :  电子邮箱文本框，跟普通的没什么区别
当输入不是邮箱的时候，验证通不过
移动端的键盘会有变化
tel   :   电话号码
url   :   网页的URL
search  :  搜索引擎
chrome下输入文字后，会多出一个关闭的X
range  :  特定范围内的数值选择器
min、max、step( 步数 )
例子 :  用JS来显示当前数值


新的输入型控件_2
number  :  只能包含数字的输入框
color  :  颜色选择器
datetime  :  显示完整日期
datetime-local  :  显示完整日期，不含时区
time  :  显示时间，不含时区
date  :    显示日期
week  :  显示周
month  :  显示月

新的表单特性和函数
placeholder  :  输入框提示信息
例子 :  微博的密码框提示
autocomplete  :  是否保存用户输入值
默认为on，关闭提示选择off
autofocus  :  指定表单获取输入焦点
list和datalist  :  为输入框构造一个选择列表
list值为datalist标签的id
required  :  此项必填，不能为空
Pattern : 正则验证  pattern="\d{1,5}“
Formaction 在submit里定义提交地址

表单验证
validity对象，通过下面的valid可以查看验证是否通过，如果八种验证都通过返回true，一种验证失败返回false
oText.addEventListener("invalid",fn1,false);
ev.preventDefault() 方法阻止元素发生默认的行为
valueMissing  :  输入值为空时
typeMismatch :  控件值与预期类型不匹配
patternMismatch  :  输入值不满足pattern正则
tooLong  :  超过maxLength最大限制
rangeUnderflow : 验证的range最小值
rangeOverflow:验证的range最大值
stepMismatch: 验证range 的当前值 是否符合min、max及step的规则
customError 不符合自定义验证
setCustomValidity(); 自定义验证

表单验证
Invalid事件  :  验证反馈 input.addEventListener('invalid',fn,false)
阻止默认验证:ev.preventDefault()
formnovalidate属性  :  关闭验证


## 新的选择器

不支持IE6，7，8

document.getElementsByClassName('class');
document.queryselector('#div');可以选中对应的元素，选用方法和jquery相似
document.queryselectorAll('.div');选中所有的class为div的元素


获取class列表属性
classList
length :  class的长度
add()  :  添加class方法
remove()  :  删除class方法
toggle() :  切换class方法 。如果写的class在元素里面出现了，就删除。没有这个class就添加

eval:可以解析任何字符串变成js
JSON.parse:只能解析JSON形式的字符串变成JS（安全性高，并且必须是个严格JSON形式）
JSON.stringify()将一个JSON解析成一个字符串，变成严格形式的json
新方法应用:深度克隆（不支持IE6，7）


课后扩展:对象的应用（浅拷贝、深拷贝）；


## 本地存储


先补充下localStorage 知识点:
JS对象
读取形式:
localStorage.name
添加/修改
localStorage.name = "xuanyuan"
其中"xuanyuan"只能是字符串形式（目前为止只支持字符串）。所以存储时是JSON对象时需要执行下JSON.stringify，所以获取时需要执行下JSON.parse
删除
detele localStorage.name

API
获取键值对数量
localStorage.length
读取
localStorage.getItem('name'), localStorage.key(i)
添加/修改
localStorage.setItem('name','xuanyuan')
删除对应键值
localStorage.removeItem('name')
删除所有数据
localStorage.clear()

顺便说下，localStorage有效期是永久的。一般的浏览器能存储的是5MB左右。sessionStorage api与localStorage相同。
sessionStorage默认的有效期是浏览器的会话时间（也就是说标签页关闭后就消失了）。
localStorage作用域是协议、主机名、端口。（理论上，不人为的删除，一直存在设备中）
sessionStorage作用域是窗口、协议、主机名、端口。

知道了这些知识点后，你的问题就很好解决了。
localStorage是window上的。所以不需要写this.localStorage，你这里的this，是指vue实例。
方案一、
// 这里写的答案是指data.body.data是JSON。不是JSON则不需要JSON.parse和JSON.stringify
存储:localStorage.data = JSON.stringify(data.body.data);
获取:JSON.parse(localStorage.data);
方案二、
存储:localStorage.setItem('data',JSON.stringify(data.body.data));
获取:JSON.parse(localStorage.getItem('data'));

