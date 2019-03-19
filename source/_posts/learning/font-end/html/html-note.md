---
title: html随笔
date: 2017-05-23 2:44:35
tags: html
categories: learning
---


<div><!-- more--></div>

## 删除线:
    1.<strike>
    2.<del>
    
## div可编辑

`contenteditable="true"`属性设置，可将div变成可编辑状态，可通过元素属性来


## 特殊符号: ##

引号:&quot  “
&reg；商标
&yen；元
&lt;小于号
&gt；大于号



## 拼音的写法: ##

    <ruby>
    拼音
    	<rt>
    		pinyin
    	</rt>
    </ruby>
    

上标:sup
下标:sub

## 预格式化: ##

pre:预格式化标签

里面是诗的话会解析换行，
按照里面写的样式来显示在浏览器上

center:居中显示文字

hr下划线



## 列表:ol有序列表 ##

倒序:
	ol中加属性:reversed
	reversed: true 
	
	属性值是true的，可以只写属性值


### 有序列表 ##

开始值 属性:start=“10” 从10个开始
类型  属性: type=“a”

type:number/a/A/i/I

### 自定义序列表: #
dl list
	dt title
		dd details
sublime快捷方式:
dl>dt+dd*4+tab

    <dl>
    	<dt></dt>
    	<dd></dd>
    	<dd></dd>
    	<dd></dd>
    	<dd></dd>
    </dl>

## a标签超链接 #

anchor:位置  -#p1, 跳转到当前id为p1的标签位置
   
    
超链接的路径:

设置绝对路径，
绝对路径指纹键的完整路径，包括文件传输的协议http、ftp等，一般用于网站的外部链接，列如:http://www.baidu.com

相对路径:
同级直接调用名称
调用下一级文件:	文件夹名称/文件名
调用上一级文件:	../文件名称       ../一次就向上跳转一次



## 表格

table
tr:行
td:列
th:表头标记  -直接加在第一行
caption:表格标题 -加在第一个table标签的下面

thead:头
tbody:身体
tfoot:尾部



table>tr*3>td*3

一个9*9的表格

### 表格的相关属性

table css reset: padding:0;table{border-collapse:collapse}单元格间隙合并，边框合并，给td，th设置border就可以给整个表格设置边框了，不过要配合border-collapse:collapse。

table的标签特性是display:table

注意事项:
1、不要给table，th，td以外的表格标签加属性
2、单元格默认评分table的宽度
3、th里面的文字默认加粗并且左右上下居中显示
4、td里面的内容默认加粗并且左右上下居中显示
5、table决定了整个表格的宽度
6、table里面的单元格宽度会被转换成百分比
7、表格里面的每一列都必须有宽度，否则就算给表格设置了宽度，当内容超过每个单元格的宽度时，会增加表格宽度
8、表格同一竖列继承最大宽度，内容可以撑开表格的高度
9、表格同行继承最大高度


colspan:规定单元格可横跨的列数，被横跨的单元格去掉
rowspan:规定单元格可横跨的行数，把被合并的单元格去掉
宽:width
边框的属性:border
边框的样式:frame、rules
设置表格的背景:bgcolor

### 设置表格的行与单元格

调整行内容水平对其---align
调整行内容垂直对其---valign
设置跨列---colspan
设置单元格间距---cellspacing 单元格和单元格的距离
设置单元格边距---cellpadding 相当于设置了宽高div的margin

valign:

baseline内容基线对齐


### 跨行设置

rowspan=“2”

给单元格设置跨行

colspan跨列设置



###换行缩进

	多行缩进
	ctrl+【；ctrl+】

## frameset集设置，里面包含多个框架

可以取代body

可以设置frame的源文件:src
添加框架名称:name
设置框架边框:farmeborder
显示框架滚动条；scrolling
调整框架尺寸:noresize

设置框架集上下分割: rows
设置框架集左右分割: cols

col=“30%,40%,300px”
col="100,*" ---- 其中*号表示减去已经分配了的大小，剩下的都对应的分配给其他frame，如果其他没设置，则*表示全部的大小距离
1040*30%

浮动框架:iframe

src:后直接加源文件



表单:提交表单，可以将表单数据提交到后台数据库。现在表单一半使用异步处理，前端进行数据妇分析


表单:数据的提交
	action : 数据提交的地址，默认是当前页面
    method : 数据提交的方式，默认是get方式
    	1.get
        	把数据名称和数据值用=连接，如果有多个的话，那么他会把多个数据组合用&进行连接，然后把数据放到url?后面传到指定页面
            url长度限制的原因，我们不要通过get方式传递过多的数据
        2.post
        	理论上无限制
    enctype : 提交的数据格式，默认application/x-www-form-urlencoded
name:表单的名称，提交表单不要给表单设置id，一般使用name来标识，


### input:

type:
1.button
2.checkbox:复选框
	disabled:禁用
	checked:默认选中
3.radio:单选按钮
4.reset:重置按钮
5.password:密码框，可以隐藏密码
6:file:插入文件域
8.submit:提交
9.hidden:隐藏域
10.selete/opstion下啦菜单
11.reset:重置
可以使用label产生关联，可以使对象之间产生关联

<label for="tel">
			联系电话:<input type="text" id="tel">
			
				<!-- 与表单控件产生关联 -->
</label>

textarea:文字域 ----自成标签
可以设置不拖动



radio--要实现单选功能

给两个同类的radio按钮:添加相同的name值


````html

	性别: <input type="radio" name="sex" >男
		  <input type="radio" name="sex">女

````

列如:


属性:
value:input元素的出事吃



单标签:！doctype\meta\br\hr\frame\input\link

双标签:meta\head\title\style\script\body\strike\strong\b\i\address\sub\sup\ruby\rt\pre\center\
ul\ol\li\dl\dt\dd\a\table\tr\td\th\thead\tbody\tfoot\caption\frameset\iframe\form\textarea\select\option\label\button


## img图片标签


### 属性:
src:图片地址
width:图片宽度
height:图片高度
alt:图片替换 --alternative替换   图片不存时显示提示文字
title:图片的标题 --将鼠标移入上去，就会显示title。并且设置了title的图片还会被收录
border:边框
title:关键词
hspase/vspase:图片间距
align:图片的对齐方式


图片宽高只设置:宽就可以了，这样高可以根据宽度的设置，等比例缩放

### 图片格式:
 


gif格式: 动画 | 图片尺寸小的时候 | 图片颜色类型比较少 （4-6）

jpeg(.jpg): 相片 | banner图、产品图、(大、颜色丰富、元素丰富、清晰)

png: 背景透明 | 图片尺寸比较小 | 颜色类型比较少
	png-8: 不保存（ie6不支持、会失真，有锯齿）
	png-24: 真实、清晰

图片质量: <=200kb(清晰)
服务器，或者网页加载图片的速度，小于等于200kb加载这些图片速度是一样的。加载大于这些图片速度就会逐渐递增。


embed:多媒体标签
插入多媒体文件

bgsound:添加背景音乐

marquee:文字滚动标签

direction:文字滚动方向


## 浏览器

	chrome(谷歌）、Mozilla Firefox（火狐）、Safari（苹果）、Opera（欧朋）、Windows Internet explorer（微软）



