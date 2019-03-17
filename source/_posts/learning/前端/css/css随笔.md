---
title: css随笔
date: 2017-05-27 8:44:35
tags: css
categories: css
---


<div><!-- more--></div>


## css概述

及层叠样式表，对网页中的元素进行样式更改。对网页中的元素进行描述的一门语言

1.内容和样式分离，使得网页设计更加趋于明了，简介。
2.弥补了html标签对属性控制的不足
3.精确的控制网页布局

## css特性
### css样式覆盖
层叠性:
当同一个标签对象，设置了同样的样式，权重高的样式会层叠低的样式


### css继承性
祖辈元素的相关属性可以继承(inherit)
1.祖辈元素的相关属性可以继承
css有很多属性可以继承:跟字体相关的属性可以继承（大小、颜色、类型、样式、粗细、行高），文本（行高、字符间距、单词间距、对齐方式、文本修饰、文本转换、段落缩进）
2.标题标签不继承:大小、粗细、
3.a标签不继承颜色
4.只有块级元素才能设置缩进

5.display属性--显示
display:block（块）
display:inline-block（行内块）


## 块标签 ##

在html中有块三种属性:行内元素（内联），块，行内块

### 常用的行内元素 ###

行内元素--元素并排在同一行显示

a\span\strong\img\em\strike\b\ruby\a\td\th\textarea\select\label\button\img


### 常用的块标签 ###

div\address\p\pre\ul\li\ol\dl\dt\dd\table\tr\caption\thead\tbody\tfoot\h1-h6\frameset\frame\iframe\form\option\hr\br

#### 行内元素的属性 ####
1.默认同行可以继续跟同类标签
2.内容撑开高度，没有内容时没有宽高
3.不支持宽高
4.不支持margin,padding （google支持marging-left，支持padding。Ie6只支持padding-left）




5.设置方法:display:inline

img底部间隙解决办法；display:block；vertical-align:top；/*top、middle、bottom*/



#### 块属性标签 ####
1.显示独占一行 
2.支持所有css
3.设置方法:display:block

#### 行内块 ####

display:inline-block可以设置
1.块在一行显示
2.行内属性标签支持宽高
3.没有宽度时内容支持宽高
4.空格没解析，空格时一个文字一半大小

兼容:
**5.ie6，ie7不支持inline-block**

### 盒子的居中

一个盒子A在另一个盒子B里水平居中显示:
解决:设置A的左右外边距值为margin:0 auto；就可以设置盒子B在里面居中显示。

如果盒子B是行内块，可以使用texe-align:center；设置盒子B在盒子A里面居中。


## 浮动 ##

### 浮动原理
浮动设置:float:left/right/none

1.使块元素在一行显示
2.使内嵌支持宽高
3.不设置宽度时内容撑开高度
4.脱离文档流（文档流时文档中显示对象排列时所占的位置，元素加了浮动，会脱离文档流，按照指定的一个方向移动，知道碰到父级的边界，或者另一个浮动元素）。
5.提升层级半层（以网页中的三维角度看，就是提升了层级关系，所以设置了浮动的元素后，没有设置浮动就会直接移动到浮动元素的下面）。

### 清浮动

为什么要清浮动？

因为我们在网页布局时，使用div，在div里面的内容使用了浮动后，就脱离了文档流，div无法获取到里面内容的高度，和宽度。尽管我们可以使用给外部div设置宽高来解决这个问题，但是这样就显得非常僵硬，无法自适应内容宽高。所以我们通过清浮动来解决自动获取宽高的问题。但这里所说的清浮动不是真正的把浮动清除，只是获取相当于没有脱离文档的状态。

清浮动的方法:


①给父元素设置高度
②给父元素设置overflow:hidden；配合zoom:1；使用
③给父元素的结束标签前面添加子元素.clear,.clear{clear:both}
④父级:.after{zoom:1}//for IE6/7s 
.father::after{content:'';display:block;width:0px;height:0px;visibility:hidden;clear:both;}
⑤给浮动元素的父级加绝对定位也可以清除浮动


1.给父级也加浮动，但是父级如果设置了margin，那么margin值将会失效
2.给浮动元素父级加display:inline-block
a.**IE6下最小高度问题**
高度小于19px元素，高度会被当作19px处理
解决办法:font-size:0，只能处理到最小2px，overflow:hidden可解决
3.在浮动元素下加
```javascript
<div style="height:0px;font-size:0;clear:both;overflow:hidden;"></div>
```
4.在浮动元素下加<br clear="all" />
5.父级:after{content:"";clear:"both";display:"block";}
  父级{zoom:1;}

6.overflow溢出也可来解决浮动的问题（因为溢出要判断对象和父级的大小关系）
auto:溢出默认出现滚动条
scroll:默认显示滚动条
hidden:隐藏滚动条
给浮动元素的父级添加
可以消除浮动，但要配合zoom:1；
7.给浮动元素的父级加绝对定位也可以清除浮动


**IE6，7元素浮动，要并在同一行的元素都要加浮动**

**浮动问题（兼容问题）**

IE6下的双边距bug
在IE6下，块元素浮动和横向的margin，横向的margin值会被放大两倍
解决: display:inline

IE6，7下li本身没有浮动，li多几px间隙问题
IE6，7下本身没有浮动，但内容浮动了li就会多几px
解决办法给li加浮动
给li加vertical-align:top；

图片添加到div中会出现底部多几px
给图片添加vertical-align:top
在IE6下高度小于19px时的元素，高度会被当作19px，处理，解决办法:overflow:hidden；



### clear

其属性值有四个clear:both|left|right|none;

简单来说呢，clear属性的作用就是“清除”浮动。

如果某元素设置clear:left;表示该元素左边不存在浮动元素

相应的，clear:right;表示该元素右边不存在浮动元素；clear:both;表示该元素两边都不存浮动元素。clear:none表示两边允许有浮动元素。

在视觉上要使某元素左边或右边不存在浮动元素,就只有它往下移一行，或浮动元素往下移一行。（这个元素肯定是不能将浮动元素清除的了,只是用这样的方式达到页面布局的效果而已）



## css使用

1.内联样式:  style标签内添加样式
2.行内样式: 在行内添加样式，style=“”  style是属性， '属性:属性值;属性:属性值;'
3.文件链接: rel:relationship -- stylesheet:样式表  href:链接的文件
4.导入式:   @import url();  url中加地址，导入式，是放在一个样式表中，导入另一个样式表。


外联语法规则: p{}  选择器{属性:属性值；属性:属性值；}

理念:结构和样式相分离，
html文件，和css文件分离开来


### 选择器
 
#### 类型:

 标签选择器 	-- a{} b{}
 类选择器   	-- .text{}  .类名{属性:属性值；}  //<div class="text" ></div>
 id选择器   	-- #div1{}  .#id名称{属性:属性名；}  //<div id="div1"></div>
 包含选择器	-- 层级关系，先父级再子元素，顺序写法
 并列选择器	-- a，p，address{}
伪类:
	a:link{} 	未访问过的状态，等价于a{}。默认blue，带下划线
	a:active{}	激活状态，鼠标按下未离开。默认blue，带下划线
	a:hover{}	鼠标悬停状态，默认红色，带下划线
	a:visited	访问过的状态。紫色，带下划线

	四个状态的顺序: 爱恨 l-o-V-e ， H-A-t-e
	
 
#### 选择器优先级:

	层叠样式:
	p{color:red;}
	p{color:blue;}
		/*层叠:后面设置的样式，会覆盖前面的样式*/

css优先关系:
	优先级越高，优先显示样式
	权重:权重的值越大，越优先显示样式 -- 

	权重值:

	行内样式style='' 			1000;
	id选择器#id{}				100;
	类（伪类）选择器.class		10；
	标签选择器p,div,span			1;
	!important					优先级最高
	

	    .a1:link{color:pink;}
    	/*1+10*/
    	.a1{color:black;}
    	/*1*/
    	span{color:yellow !important;}
    	#one span{color:black;}
    	/*100+1=101*/
    	div .one ul li span{color:blue;}
    	/*1+10+1+1+1=14*/
    	div 
    	ul li span{color:orange;}
    	/*1+1+1=3*/
    	li span{color:green;}
    	/*1+1=2*/
					

	行内样式>id选择器>类选择器>包含选择器>标签选择器

## 字体:
	
	font-family:"黑体"

	火狐、谷歌、Safari默认字体:微软雅黑   
	字体大小:谷歌、火狐默认渲染的字体大小是16px
	谷歌:最小支持12px



	IE:宋体
	所有浏览器:'Arial'
	font-family: 'Arial','宋体','毛泽东行书';
	一个个的字体往后读取，如果第一个不可以使用，则往后读取，直到可以执行为止。英文字体放在前面，英文字体不支持中文。
	
	
	font-size:绝对尺寸 | 相对尺寸 |
	设置绝对尺寸，要加上单位，如果没有加单位，浏览器默认以px为单位，绝对尺寸可以使用的单位包括in（英寸），px（像素），pt（点），cm（厘米），mm（毫米），pt（点）、pc（皮卡）。
	
	相对单位:
	em:相对于父元素。来计算。离设置这个字体最近的父元素。
	200%:相对于父元素。来计算。这个字体的大小
	
	
	font-ver
### 字体样式: 

font-style:
	normal:正常显示
	italic:斜体显示文字
	oblique:歪斜体显示
font-weight: 
	normal|bold|bolder|lighter|number
	normal:		正常粗细
	bold:		粗体(粗体是700)
	bolder:		加粗体
	lighter: 	细体
	number:		数字一般是整百，有九个级别:100-900
font-variant:
	normal|small-caps
	normal:正常字体；默认字体样式
	small-caps:小写字母转换成大写字母，并且缩小
font:
	font:italic bold 30px/40px '楷体';  30px/40px(指代字体大小和行高)

### 文本修饰属性

letter-spacing: 
	文字间距
word-spacing:
 	单词间距
text-decoration:
	underline|overline|line-through|blink|none
### 文本的对齐方式


text-align:
	left|right|center|justify	--水平对齐
	justify:两端对齐

### 文本缩进

text-indent:
	2em

### 文本行高

line-height:
	normal:默认的行高
	number:


### 大小写缩写开始
text-transform:
	uppercase；全部大写
	lowercase;全部小写
	capitalize；首字母


## 背景

background-color: 		#fff; 	--背景色
background-image: 		url();	--图片背景
background-repeat:		repeat; --默认取值平铺，(repeat-x:横向平铺，repeat-y:竖向平铺，no-repeat:不要平铺)
background-position:	/*left top；--默认，左上，（right top:右上，center top:中上，center bottom:中下）
						可以输入数值left:  top:，两个参数可以确定距离左边，距离上边的距离*/
background-attachment:	scroll;	--默认滚动，（fixed:固定图片的位置）
background: #ffffff url(images/img1) center center fixed  no-repeat;颜色、地址、位置、附着、重复

## 不同的浏览器会给网页的元素设置不同的默认样式

user agent stylesheet用户代理（浏览器）样式表

ul小圆点，a标签的下划线、颜色，谷歌浏览器的字体大小16px，

### 构建自己的样式重置表



## 盒子模型

概念:盒模型指的是HTML里面的元素的内容（content）的宽度（width）和高度（height）、内边距（padding）、边框（border）和外边距（margin）所占据的区域

IE盒子模型大小:content+padding+border+margin    实际大小:content+padding+border；IE浏览器5、6
标准盒子大小:content+padding+border+margin      实际大小:content

属性:width、height、padding、border、margin
内边距 内补丁、内填充
外边距 外补丁、外填充

盒子在水平方向居中显示:
margin:0 auto；可以设置居中

上外边距的转移:
问题:子元素的上边距转移给了父元素
解决办法:给父元素设置:
overflow:hidden
溢出:隐藏




组成:快标签宽高、padding、border、margin

### padding:内边距

1.padding: top right bottom left; 顺时针的顺序 
2.三个值（顺时针）   padding:1px 2px 3px；  1px--上  2px--左右 3px-下
3.两个值 padding:1px 2px;  1px -- 上下  2px--左右
4.一个值 padding:1px； 上下左右都是1px

### border 边框

border:1px； 上下左右
border-top-width:2px;
border-top-style:solid;
border:width solid color；
border-top:2px solid black；

实线:solid
虚线:dashed
点状线:dotted
双边线:double


## list-style列表属性:

list-style-position

list-style-image

## cursor鼠标指针

属性值:

auto:自动获得
pointer:手型
help:帮助
move:移动


## 图片自适应宽度

给包裹图片的父元素，设置宽度。最后给图片设置百分比宽度	

### 图片自适应宽度

给包裹图片的父元素，设置宽度。最后给图片设置百分比宽度

### 定位

问题:元素A需要放在元素B上面，
解决:	给元素A做定位，position:absolute；position:inherit;
		给元素A的父元素C做相对定位
例子:ol需要放在ul上面，给ol做绝对定位，给ul做绝对定位
原理:子绝父相
定位元素，默认后者层级高于前者

浏览器默认定位:static静态定位
没有加定位就会忽略:top、bottom、left、right。z-index
z-index:只用给1，就可以在最上层了


相对定位:
a.占用文档流，相对于自身进行定位；
b.不影响元素的特性，该是块还是块，该是内嵌还是内嵌
c.父级的overflow:hidden；保不住子集的相对定位。iE6下



绝对定位:
a.从文档流中删除，相对于自身的父级进行定位。
b.若父元素没有设置定位（出static外），则继续向上寻找
c.使内联支持宽高
d.块属性标签内容撑开宽高（如果没有设置宽高的情况），还是支持宽高
e.后面的元素加了定位的层级会比前面高，绝对定位元素层级会比没有加定位的元素层级高，而没有
兼容:ie6下定位元素的父级的宽高都为基数的话那么在ie6下定位元素的right，bottom都有1像素的偏差



固定定位:
a.从文档流中删除，相对于浏览器窗口进行定位
b.块属性标签内容撑开宽高（如果没有设置宽高的情况），还是支持宽高
c.使内联支持宽高
兼容问题:不支持IE6，并且ie6下，如果父级包含的子集，子集大于父级，则撑开父级大小

层级属性:z-index

#### displaty:none 与visiblility:hidden的区别

display:none，会在文档流中删除对象

visibility:hidden；会隐藏对象，但是还在文档流中，占据位置

图片之间的间隙:border:0px;


### css优化

概念:提高效率

1.外边距简写: margin:10px； 上下左右都一样 ，两个一样

2.内边距简写: padding:10px； 上下左右都一样

3.背景属性: 颜色、图片平铺方式、fixed、图片开始位置

4.属性简写-字体:
font-italic bold 15px、20px  ‘微软雅黑’

字体属性简写:必须写字号，与字体名称必须填写

5.选择器的优化
	ID选择器最快
	class 很快
	元素	块
属性继承，减少选择器
.box{padding:10px;}
.box p{color:#333;}
简写为 .box{padding:10px;color:#333;}



简化选择器
ul.list li a{border:1px solid #ccc;}

简化为: .list a{border:1px solid #ccc;}

### display嵌套规则

块元素内包含所有行内元素
行内元素不能包含块元素
一下元素不能包含块元素h1-h6，p，span




## 版心


留白区域，增加一些附加东西。左右两边，广告什么的。

版心，如何实现，在页面改动的时候，内容一直留在版心里面


### 边框弧度

把对象的宽高设置成一样，然后给border-radius:50%；就可以设置成圆形

##瀚方手机网站


查看图像的大小


## 页面布局

概念:一个元素需要放在另外一个元素上面，给元素定位。确定元素的位置，可以脱离文档流
定位原理，子绝父相
主属性:position
属性值: fixed（固定定位）、absolute（绝对定位）、relative（相对定位）

配合属性:left\top\bottom\right

注:以上四个元素只有在做了定位时，才有效

文字在垂直方向居中显示:
办法:把元素的高度和行高设置成一样的值




## 页面布局

概念:一个元素需要放在另外一个元素上面，给元素定位。确定元素的位置，可以脱离文档流
定位原理，子绝父相
主属性:position
属性值: fixed（固定定位）、absolute（绝对定位）、relative（相对定位）

配合属性:left\top\bottom\right

注:以上四个元素只有在做了定位时，才有效

文字在垂直方向居中显示:
办法:把元素的高度和行高设置成一样的值

