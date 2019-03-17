---
title: jQuery
date: 2017-07-25 7:28:35
tags: jQuery
categories: js
---


<div><!-- more--></div>

## jQuery简介

$()方法产生的jQuery对象，不管也不论找没找到，找到了几个，得到的都是一个类数组对象，只是length值不同而已

1.js: 函数绑定时赋值
jQ:函数绑定都是传参的
```javascript
$(function(){
	alert(1);
});
==
$(document).ready(function(){
	alert(1);
});
```
2.以原声javascript方法找到的东西是javascript对象
以$()这个函数产生的东西是jQuery对象
各自类型的对象只能调用各自体系的相应属性和方法，不能穿插调用

jQuery对象可以和javascript对象进行相互转化

javascript转jQuery:使用$(javascript对象)
jQuery对象转javascript对象:[]下标法，或get(index)

3.jQuery对象进行操作内含迭代操作？？
each函数迭代是，迭代出来的全是javascript对象，事件回调函数中的this是javascript对象,$(this):jQ的this
$('input').each(function(i,v){
//里面的v是javascript对象,i是下标，$(v)变成了jQ对象
$(v)
});


## jQuery查找

$('#id'):找到id名为id的节点，找到的结果是一个jQuery创建的对象，是一组，不过通过id只能找到的是一个
$('.class'):找到class名为class的节点，多个
$('table'):找到tagName为table的标签
$('tagName[proto=""]'):找到标签名为tagName并且有一个proto属性，值为空的节点
$('[proto=""]'):找到所有有proto属性的并且等于空的节点
$('[proto]'):找到所有有proto属性的节点
$(':button'):找到所有type为button的input
$('ul li:first'):找到第一个ul下的第一个li
$('ul li:first-child'):找到所有ul下的第一个li
$('tr:even'):选取偶数位置的tr
$('tr:odd'):选取奇数位置的tr


1.一般
$('#one'):id选择器
$('.div'):class选择器
$('div'):标签选择器
$('*'):统配选择器

2.子代
$('.one div'):后代选择器==$('.one').find('div');
$('.one>*'):子元素选择器
$('.one').children():找到class为one的所有子元素

3.兄弟选择器
后面紧挨着的兄弟选择器
$('#one+div'):找到紧挨着的div兄弟，如果不是div就没找到==$('#one').next('div')

后面所有的兄弟
$('#one~div'):找到#one后面所有为div的兄弟元素==$('#one').nextAll('div')

前面紧挨着的兄弟
$('#two').prev('div'):前面紧挨着的一个div兄弟
前面所有兄弟
$('span').prevAll():前面所有的兄弟
除自身外的所有兄弟
$('#two').siblings()


4.过滤选择器之基本过滤
:first选第一个
$('div:first');找到所有div的第一个元素==
$('div').filter(':first')

注意:子元素的过滤选择器的编号从1开始，
子元素过滤选择器前面要加空格，否则结果不可预知

$('div :first-child'):没有兄弟的选择器，只有一个元素

$('div :last');找到所有div的最后一个元素

$('div :nth-child(1)');找到所有div里面的第一个子元素

$('div :nth-child(odd)');找到所有div里面为奇数的元素
$('div :nth-child(even)');找到所有div里面为偶数的元素
$('div :nth-child(2,3)')找到div里面的第2，第3个子元素

特别注意:n从0开始进行依次计算，但子元素任从1开始编号
$('div :nth-child(3n)');3的倍数
$('div :nth-child(n+2)');div里面从第3个及第三个后面的	
	


:odd选奇数位置(从0开始奇数)
$('div:odd')
:even选偶数位置(从0开始奇数)
$('div:even')

eq()选取指定位置(从0开始计数，equal)
$('div:eq(5)'):找到第五个div

lt()选取小于指定位置的元素(从0开始计数)
$('div:lt(5)'):选取小于5位置的所有div
gt()选取大于指定位置的元素(从0开始计数)
$('div:gt(5)'):选取大于5位置的所有di

not()选取不符合条件的元素
$('div:not(.one,.mini)'):先选中所有的div，然后找到所有class不为one或mini的div

:header选取所有的h标记
$('#one :header');表示id为one下面的h标签

:animated选取所有正在执行动画的元素

:hidden选取页面中所有看不见的元素
设置了display:none或visibility:hidden;或 input中type为hidden的元素

:visible选取所有可见元素                         


5.过滤选择器之内容选择器
:empty选取没有任何子元素，也没有文本的元素
$('div:empty'):找到div中没有子元素，也没有文本的

:parent选取包含了后代元素，或文本的元素
$(':parent'):找到所有包含了后代元素或文本的标签

:has()包含符合条件后代元素的元素，子代满足条件的父级
$('div:has(.mini'):找到了有子元素并且有class名为.mini的父元素div

:contains('内容'):内容满足条件
$('div:contains("te")');找到内部内容有te，或者内部子元素内容有te的div


6.过滤选择器之属性过滤

[属性名]找到了指定属性的元素
$('div[title][id]');找到的div既有title属性，又有id属性

[属性名='指定值']
$('[title="test"]');找到属性名为test的标签

[属性名!='指定值']
$('[title!="test"]');找到属性名没有test，并且值为test的元素

[属性名^='指定值']指定属性值以指定值开头的元素
$('[title^="te"]');

[属性名$='指定值']指定属性值以指定值结尾的元素
$('[title$="sst"]');

[属性名*='指定值']指定属性值以包含指定值的元素
$('[title*="sst"]');


7.过滤选择器之表单过滤

:input找到所有表单元素
:text找到所有type为text的表单元素
:button找到所有type为button的表单元素
:radio找到所有type为radio的元素
:checkbox找到所有type为checkbox的元素

过滤选择器值表单过滤选择器
checked:为radio、checkbox服务
$(':radio:checked'):找到表单中单选按钮被选中的元素
$(':checkbox:checked'):找到表单中多选按钮被选中的元素


selected:为select表单元素服务
$('select:option:selected'):找到表单中option被选中的元素


## jQuery对dom节点进行操作

### 创建和插入
1.创建和插入
$('<p></p>').text('内容').appendTo('body');添加在原来内容的后面，对应append，内容写在后面
$('<p></p>').text('内容').prependTo('body');添加在原来内容的前面，对应prepend，内容写在后面
```javascript
$('<p>内容</p>').insertBefore('p');== 
$('p').before($('<p>内容</p>'));
```
```javascript
$('<p>内容</p>').insertAfter('p');==
$('p').after($('<p>内容</p>'));
```

### 删除节点

$('p').remove();删除了自己，返回被删除的本身，jQ函数调用后，返回的都是调用者本身
remove()函数可以接收参数，过滤被删除的元素

$('p').empty();删除子元素


###克隆
(可以选择是否克隆事件)
$('p').clone(true).appendTo('div');
clone函数的参数为true时，把对象的事件也克隆过去，默认为false，不克隆事件，只克隆html标签

### 修改、获取值

html()函数、text()函数:给值修改，不给值获取
获取value值:val()函数:给值修改，不给值获取
addCalss();removeClass();增加修改class
$('p').attr('data','001');设置属性值
$('p').attr('data');一个值读取属性
css()函数
单个样式设置:$('p').css('color','red');
批量设置:
$('p').css({
	"color":'red',
	"background-color":'black'
});

### 包裹操作

6.wrap()被包裹	wrapAll():全部包裹	wrapInner():包裹里面的内容
$('p').wrap('<strong></strong>');


## 事件绑定

jQuery的事件体系只支持事件冒泡，不支持事件捕获，如果一定要事件捕获请使用原始的javascript中的addEventListener进行捕获
$('input').on('click',{key:'zhouxiao'},function(e){
	console.log(e.data);
}).off('click');

on:可以实现兼容的绑定事件，
off:解绑事件

e.data;可以获取绑定时候传过来的值
e.stopImmediatePropagation();阻止马上要发生的时间
e.stopPropagation();停止冒泡
e.preventDefault();阻止默认事件
return false;//这样既可以阻止冒泡也可以阻止默认行为

e.target;目标事件源对象


e.pageX、e.pageY;相对于浏览器可视区的偏移量

e.relatedTarget;相关联的
fromElement	toElement(移出、移入事件):IE下，
relatedTarget:非IE
e.which


jQuery中的事件合成
1.hover合成的是mouseenter和mouseleave


2.toggle合成了点击时的切换(不给参数，在可见于不可见之间切换)
$('input').on('click',function(){
	$('div').toggleClass('b'); 
});//每次点击input让，div在有class‘b’，和没有class‘b’之间切换

$('input').on('mouseover mouseout',function(){
	$(this).toggleClass('a');
});//移入移出来回切换有没有class‘a’


3.事件模拟
focus:焦点事件
$('input').trigger('focus');//让input获取焦点,会添加默认行为
$('input').triggerHandler('focus');//触发它的处理，不给焦点样式
$('input').select();选中了input里面的内容


4.事件的命名空间(范畴)

$('input').on('click.zhang',function(){

});
$('input').on('click.li',function(){

})
$('input').on('click',function(){

});
$('input').off('.zhang').trigger('click');//将所有张三绑定在input上的事件去掉


5.我们可以通过on来绑定自定义的事件，但只能通过trigger或triggerHandler来模拟触发

				
				
```javascript
$(document).on('contextmenu',function(e){
	e.preventDefault();
});//阻止浏览器右击的默认行为

$(document).on('dblclick',function(e){
	e.preventDefault();
});//双击左键

$('input').one('click',function(){
	alert(1);
});//绑定一次

$('input').on('mouserover',function(e){
	alert(1);
}).on('mouserout',function(e){
	alert(2);
}); ==
$('input').hover(function(){
	alert(1);
},function(){
	alert(2);
});
```


## 动画

jQuery动画相关的关键字:slow、normal、fast	
.hide、.show,高度和透明度变化
fadeIn、fadeOut:淡入、淡出
slideUp与slideDown:slideToggle()

animate:三个参数:对象字面量的动画参数、时间、
使用stop停止动画

stop函数如果不给参数默认只能停止元素当前正在执行的动画，和元素相关的后面的动画还是会执行:
两个参数，
第一个参数用来控制结束动画的数量（默认false，只清除当前动画，true清空元素动画的队列),
第二参数（是否让元素直接达到动画状态结束，默认false），正在执行动画达到最终状态

就算正在执行的动画提前被结束，也会执行动画的回调函数(如果你设置了)

如何判断元素是否处于动画状态
$('target')is(':animate');