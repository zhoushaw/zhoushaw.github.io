---
title: css3
date: 2017-06-12 8:07:44
tags: css3
categories: css
---


<div><!-- more--></div>

##居中方式
* `position:absolute;margin:0;left:0;top:0;right:0;bottom:0;`
* `position:absolute;left:50%;top:50%;transform:translateX(-50%) translateY(-50%);`
* `display: flex;justify-content: center;align-items: center;`

## 推荐网站

花瓣网

##选择器

属性选择器:
 
E[attr]			--表示选择所有带有attr属性的E元素

E[attr~=val]  	--表示的一个单独的属性值，这个属性值是以空格分隔开的
 
E[attr|=val]	--表示的[attr|val]属性值就是“value”，或者以“value”开始并立即跟上一个“-”字符，也就是“value-”。比如lang=“zh-cn”

E[attr*=val]	--表示的属性值里包含val字符并且在“任意”位置

E[attr^val]		--表示的属性值里包含val字符并且在“开始”位置，后面没有别的属性也可以

E[attr$val]		--表示的属性值里包含val字符并且在“结尾”位置，属性只有一个值。也属于最后一个


伪类选择器:从1开始计数

E:first-child			--相对于父级作参考，“所有”子元素的第一个子元素，并且“位置”
E:nth-child(n)			--匹配父元素中的第n个子元素E，并且这个元素得是E标签
E:nth-child(odd)		--奇数元素
E:nth-child(even)		--偶数元素
E:nth-last-child(n)		--匹配父元素中的倒数第n个子元素E
E:nth-of-type(n)		--匹配某一类中的第n个兄弟元素E
E:nth-last-of-type(n)	--
E:last-child	
E:first-of-type
E:only-child			--陪陪属于父元素中唯一子元素的E
E:only-of-type			--陪陪属于同类型中唯一兄弟选择器

选择器:

“>”		:直接子代选择器 		        --找到下一级子元素，不能向下继续找

“+”		:直接后面的一个兄弟			
--直接从后面找，找到兄弟。没有找到停止. span:nth-child(1) + span{margin-left:30px;}先找到span的父级，在这个父级里面找到第一个span，再找到最接近这个span的另一个span元素，这个就是要找的元素。如果 span + span{margin-left:30px;}给这个父级里面每一个span设置margin-left。除第一外，因为从第一个开始找

“~”		:直接后面所有兄弟选择器	
--作用于后面的兄弟元素，找到指定元素后面所有的对应元素 ul li~li，找到ul第一个元素，后面的所有元素第一个除外

">、+、~"权重值是0，但是优先级更高，
.nav li~li{background:blue;}	.nav ul li li {background:pink;}	使用~，>,+,的元素优先级更高
	

目标伪类:

target:匹配相关URL元素、哈希值里面的东西

文本伪类:
E:first-line:			表示这文字的第一行文本
E:first-letter:			表示E的第一行文字，第一个文字选不中
E:selection:			表示E的文本被选中时的状态		



表单控件:
enabled:可点击状态
disabled:不可编辑状态
checked:复选框状态



## 颜色属性

opacity:滤镜				--子元素会继承父元素的透明度



RGBA:颜色可以透明


hsla(0,10%，10%,0.3）		--

length:色调。0-360
h:颜色
s:色彩饱和度
l:亮度
a:透明度
percentage




## 伪元素

伪元素可以使用一个‘:’，也可以使用两个‘:’


p::after{content: 'abc';}		--在p标签内容后面添加‘abc’内容

p::before{content:'ABC';}		--在p标签前面添加ABCD
p:not(.p2){}					--排除掉class为p2的p标签


attr(属性)，在样式设置里面可以设置，找到里面的属性的值。




## 边框:

border-radius:边框圆角		--边角变圆，是因为。边角有内切圆。这个圆的大小设置的是，border-radius设置的是圆的半径，如果有边框宽度，加上边框宽度
上右下左: 左上、右上、右下、左下

椭圆 border-radius

椭圆:宽度是高度的一倍 --border-radius:宽 / 1/2宽;
椭圆:宽度是高度的一半 --border-radius:宽 / 2宽;

### 边框图片

border-image:image、number、perceage、
border-style:solid（必加）、
border-image-width:10px
border-image-source:url（）
border-image-width:
border-image-slice:对应值，将图片切成九部份对应部分为对应部分的值
四个对应的值:图片顶部、右侧、底部、左侧内偏移量
border-image-repeat:
round 平铺,repeat 重复,stretch拉伸 




#### box-shadow

border-shadow:阴影 3个值		【inset】内投影	X轴偏移量，Y轴偏移量、模糊度、扩展量（可不写），颜色
原理:阴影就是，这个盒子下面增加增加了一个颜色的块，它是绝对定位的。当x偏移量就相当于left值，y偏移量就相当于top值，扩展值就是给下面盒子增加的宽高值。


X轴偏移量:正值从右边框开始			--负值从左边开始
Y轴偏移量:正值从下边框开始			--负值从上边开始
哪边不需要阴影将对应的阴影设置0

偏移量和模糊度可以相加计算，负号只能代表方向
扩展量:偏移量，偏移的距离


#### 内阴影




psd文件，右击图层->混合选项->阴影		--可以查看对应的距离、


## 盒模型

盒模型:是用来设计和布局使用的，实际上它包括外边距、内边距、边框、内容
IE盒模型:	内容+padding+border = width		IE盒模型只会出现在IE5，和IE6以上怪异模式中


css3盒模型:
box-sizing:
content-box，以前使用的是这种盒模型，盒子的宽高内容:+padding+border = width。padding增加，宽增加，border增加、盒子增加
border-box，边框盒模型，盒子宽等于width+padding+border，增加padding减少内容宽高，增加border减少宽高。

### 弹性盒模型
注意在使用弹性盒模型的时候 父元素必须要加display:box 或 display:inline-box
Box-orient 定义盒模型的布局方向
Horizontal 水平显示
vertical 垂直方向
box-direction 元素排列顺序
Normal 正序
Reverse 反序
box-ordinal-group 设置元素的具体位置

Box-flex 定义盒子的弹性空间
子元素的尺寸=盒子的尺寸*子元素的box-flex属性值 / 所有子元素的box-flex属性值的和 

### 富裕空间管理


box-pack 对盒子富裕的空间进行管理
Start 所有子元素在盒子左侧显示，富裕空间在右侧
End 所有子元素在盒子右侧显示，富裕空间在左侧
Center 所有子元素居中
Justify 富余空间在子元素之间平均分布

box-align 在垂直方向上对元素的位置进行管理
Star 所有子元素在据顶
End 所有子元素在据底
Center 所有子元素居中


box-reflect 倒影
direction  方向     above|below|left|right;
距离
渐变（可选）
resize 自由缩放
Both 水平垂直都可以缩放
Horizontal 只有水平方向可以缩放
Vertical 只有垂直方向可以缩放
注意:一定要配合overflow:auto 一块使用只有水平方向可以缩放



##文本

text-shadow:x偏移 y偏移 模糊程度 颜色;		--10px 10px 10px red;
text-stroke:大小 颜色;描边
direction:ltr;从左到右。rtl从右到左配合unicode-bidi使用

### 自定义字体

可以查找

使用ai制作字体，然后通过http://www.fontsquirrel.com/fontface/generator

### 自动换行


word-wrap:
normal:到屏幕的边缘自动换行，一个单词如果屏幕边缘占不下也会自动换行
brder-all:只有要盒子占不下了就会换行，不会管单词的长度
break-word: 如果文本到达盒子边缘时自动换行，单词放不下了，先换行在打断


### white-space

pre:按照你在html里面写的格式一样，会解析空格，和换行符
norml:多个空格解析成一个空格
pre-wrap:把文字限制正在父级里面，但是还是会解析空格
preline:文字里面的空格会解析

nowrap:多个空格解析成一个空格




text-overflow:ellipsis；文字溢出显示为省略号
配合nowrap和overflow:hidden使用


多行超出宽度自动隐藏:

display:-webkit-box;
-webkit-line-clamp:5;
-webkit-box-orient:vertical;
overflow:hidden;
text-overflow:ellipsis;


## 背景

background-clip:

padding-box，从内边距开始显示背景色
border-box，从边框区域开始显示背景色
content-box，从内容区域开始显示背景色
text


background-origin:	背景原点。默认从内边距开始

border:从border区域开始显示背景
padding:从padding区域开始显示背景
content:从content区域显示背景



background-size:
cover:覆盖，如果图片不够大，也拉伸覆盖起来，铺满整个容器。会使最大边，进行缩放，另一边同比缩放，超出部分会溢出
contain:会使最小边，进行缩放


多重背景:4
background-image:url（） left top ， url（） left top ， url（） left top ，url（） left top ；


### 渐变:

background-image:
线性渐变:linear-gradient(color,color,...);

角度:linear-gradient（角度，color 百分比（宽度），color 百分比（宽度），...);

从上到下:180；从下往上0；从左往右90，从右往左270。（原理，像一个时钟在中心位置，按顺时针旋转)
从下往上:to top，右下到左上 to left top，左上到右下:135deg、 to right bottom


## 浏览器前缀

-webkit:chrome
-o:opera
-moz:火狐


JS中写法:WebkitTransition、MozTransition、OTransition


## Transition

transition-property  要运动的样式  （all || [attr] || none）
transition-duration 运动时间
transition-delay 延迟时间
transition-timing-function 运动形式 
ease:（逐渐变慢）默认值
linear:（匀速）
ease-in:(加速)
ease-out:（减速）
ease-in-out:（先加速后减速）
cubic-bezier 贝塞尔曲线（ x1, y1, x2, y2 ） http://matthewlein.com/ceaser/

### Transition过渡完成检测

过渡完成事件 
Webkit内核: obj.addEventListener('webkitTransitionEnd',function(){},false);
firefox: obj.addEventListener('transitionend',function(){},false);

清除end事件

Webkit内核: obj.removeEventListener('webkitTransitionEnd',function(){},false);
firefox: obj.removeEventListener('transitionend',function(){},false);

function removeEventListener(obj,fn){
		obj.removeEventListener('webkitTransitionEnd',fn,false);
        obj.removeEventListener('transitionend',fn,false);
}


## 2d 转换


### transform

transform
rotate()  旋转函数 取值度数
deg  度数
Transform-origin 旋转的基点
skew() 倾斜函数 取值度数 
skewX()
skewY()
scale() 缩放函数 取值 正数、负数和小数
scaleX()
scaleY()
translate() 位移函数
translateX()
translateY()


修改旋转，缩放的中心点

transform-origin:left top;


### Matrix

matrix(1,0,0,1,0,0)
	matrix(a,b,c,d,e,f);
	progid:DXImageTransform.Microsoft.Matrix( M11= 1, M12= 0, M21= 0 , M22=1,SizingMethod='auto expand');
	Matrix( M11= a, M12= c, M21= b , M22=d,SizingMethod='auto expand');
	位移:
	x:e+disX
	y:f+disY
	
	缩放:
	x轴缩放 a=x*a   c=x*c;
    y轴缩放 b=y*b   d=y*d;
	
	x轴斜切: c=Math.tan(xDeg/180*Math.PI)
	y轴斜切: b=Math.tan(yDeg/180*Math.PI)

	
	a=Math.cos(deg/180*Math.PI); 
	b=Math.sin(deg/180*Math.PI);
	c=-Math.sin(deg/180*Math.PI);
	d=Math.cos(deg/180*Math.PI);


旋转兼容已封装的函数:

function toRotate(obj,iDeg)
{
	var a=Math.round(Math.cos(iDeg/180*Math.PI)*100)/100;
	var b=Math.round(Math.sin(iDeg/180*Math.PI)*100)/100;
	var c=-b;
	var d=a;
	obj.style.WebkitTransform="matrix("+a+","+b+","+c+","+d+",0,0)";
	obj.style.MozTransform="matrix("+a+","+b+","+c+","+d+",0,0)";
	obj.style.transform="matrix("+a+","+b+","+c+","+d+",0,0)";
	obj.style.filter="progid:DXImageTransform.Microsoft.Matrix( M11="+a+", M12= "+c+", M21= "+b+" , M22="+d+",SizingMethod='auto expand')";
	obj.style.left=(obj.parentNode.offsetWidth-obj.offsetWidth)/2+"px";
	obj.style.top=(obj.parentNode.offsetHeight-obj.offsetHeight)/2+"px";
}


## 3d变换

张鑫旭前端大牛

transform-style（preserve-3d） 建立3D空间
Perspective 景深
Perspective- origin 景深基点
Transform 新增函数
rotateX()
rotateY()
rotateZ()
translateZ()
scaleZ()

### animation

关键帧——keyFrames
类似于flash
只需指明两个状态，之间的过程由计算机自动计算
关键帧的时间单位
数字:0%、25%、100%等
字符:from(0%)、to(100%)
格式
@keyframes 动画名称
{
	动画状态
}

可选属性
animation-timing-function	动画运动形式
linear	匀速。
ease		缓冲。
ease-in	由慢到快。
ease-out	由快到慢。
ease-in-out	由慢到快再到慢。
cubic-bezier(number, number, number, number):	特定的贝塞尔曲线类型，4个数值需在[0, 1]区间内

可选属性(2)
animation-delay			动画延迟
只是第一次
animation-iteration-count		重复次数
infinite为无限次
animation-direction			播放前重置
动画是否重置后再开始播放
alternate	动画直接从上一次停止的位置开始执行
normal	动画第二次直接跳到0%的状态开始执行
animation-play-state:(running,paused)


animation-name	指定要绑定到选择器的关键帧的名称
animation-duration	动画指定需要多少秒或毫秒完成
animation-timing-function	设置动画将如何完成一个周期
animation-delay	设置动画在启动前的延迟间隔。
animation-iteration-count	定义动画的播放次数。
animation-direction	指定是否应该轮流反向播放动画。
animation-fill-mode	规定当动画不播放时（当动画完成时，或当动画有一个延迟未开始播放时），要应用到元素的样式。
animation-play-state	指定动画是否正在运行或已暂停。
initial	设置属性为其默认值。 阅读关于 initial的介绍。
inherit	从父元素继承属性。 阅读关于 initinherital的介绍。


animation检测函数,可以检测到函数是否已经结束了

function addEnd(obj,fn){

obj.addEventListener('webkitAnimationEnd',fn, false);
obj.addEventListener('animationend', fn, false);
}


