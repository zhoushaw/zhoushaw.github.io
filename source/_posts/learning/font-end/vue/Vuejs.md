---
title: Vue.js
date: 2017-08-11 8:52:35
tags: js
categories: js
---


<div><!-- more--></div>


## Vue简介

vue是一个mvvm框架,
使用vue都要有一个Vue的根实例(有且只有一个)
Vue的实例对象，通过new Vue()都是Vue的实例对象(本身是其data属性值的代理)
挂载mount
vue框架核心:从复杂枯燥的dom操作中解放出来，我们只需挂心我要现实哪些数据，这些数据由谁来怎么显示!!!我们如果想操作dom我们只需操控数据


## Vue实例创建



```javascript
<div id="app>
	<show></show>	
</div>


//这样就构建了一个简单的模板
<template id="show">
	<p>这是一个模板</p>
</template>


//声明了一个叫做show的模块
var show = Vue.extend({
	template:'#show'
});
//将这个组件注册在全局
Vue.component('show',show);


var vm =new Vue({
	el:'#app',
	data:{},
	methods:{},
	computed:{},
	created:{},
	componets:{},

});

```

## Vue模板语法

Vue实例，以下都是通过这个实例实现的:

```javascript
var vm = new Vue({
	el:"#app",
	data:{
		msg:new Date(),
		flag:true,
		data:['王五','李四','quni']
	},
	methods:{
		//methods
		del:function(item){
			this.data.splice(this.data.indexOf(item),1);
		}
	}
});
```

1.v-text:加入指定的内容

```javascript
<div id="app">
	今天的日期是: <span v-text="msg"></span>
</div>
```

2.
v-if="flag":加一个boolean值，如果为真是显示,并且在文档中
v-else="flag"的与v-if相反(v-if="!flag")，不在文档中
v-show="flag":显示，
v-show="!flag"不显示，dipslay:none

v-show与v-if:
a.v-show指令表示的元素，无论true或false都要加载到页面中，只是显示不显示的区别，这样初始加载成本就高，但是来回频繁切换就节约了成本，所以适合在频繁切换的标签上使用v-show，
b.而v-if指令表示的元素，只有true才会被加载到文档中，不为  true则vue实例不做任何处理，这样就节约了初始加载成本，但若以后要切换则要重新编译回载，切换成本高



3.template，在实际的dom中不会显示这个，可使用这个批量操作，隐藏等:,并且template只能配合v-if使用，不能配合v-show使用
实例:

```javascript
<ul>
	<li v-show="flag"></li>
	<li v-show="!flag"></li>
	<template v-if="flag">
			<li>菜单1</li>
			<li>菜单2</li>
			<li>菜单3</li>
	</template>
	<li>菜单4</li>
	<li>菜单5</li>
	<li>菜单6</li>
</ul>
```


4.v-for="n in 10" v-text="n",会创建10个li，内容1-10，n从1开始
实例:


```
<ul>
	<li v-for="n in 10" v-text="n"></li>
</ul>

<ul>
	<li v-for="(item,index) in names">
		<span v-text="index"></span><span v-text="item"></span>
	</li>
</ul>
//item:显示的数据，index对应下标
```



5.v-bind:可以绑定自己需要的值，使用vue绑定的数据(简写:':')

v-on:click绑定事件使用methods里面的方法(简写:'@')

实例:

```javascript
<table>
	<tr v-for="item in data">
		<td v-text="item"></td>
		<td>
			<a href="#"  v-bind:data-id="item" v-on:click="del">del</a>
			<!-- 要想在调用这个函数并且把事件对象传进去(e||window.event),传$event -->
		</td>
	</tr>
</table>
```	

实例二:

```javascript
<table>
	<tr v-for="item in data">
		<td v-text="item"></td>
		<td>
			<a href="#" v-on:click="del(item)">del</a>
		</td>
	</tr>
</table>
```

6.表单绑定数据

```javascript
<form action="">
	<input v-model="name" type="text">
	<input v-model="pwd" type="possword">
	<input name="sex" v-model="sex" type="radio" value="male">男
	<input name="sex" v-model="sex" type="radio" value="famale">女
	<input name="hobby" v-model="hobby" type="checkbox" value="eat" >吃饭
	<input name="hobby" v-model="hobby" type="checkbox" value="sleep" >睡觉
	<input name="hobby" v-model="hobby" type="checkbox" value="dadoudou" >打豆豆
	<input name="hobby" v-model="hobby" type="checkbox" value="play" >玩游戏
	<select name="" id="" v-model="address">
		<option value="Beijing">北京</option>
		<option value="Shanghai">上海</option>
		<option value="Guangzhou">广州</option>
	</select>
</form>	

var vm = new Vue({
	el:"#app",
	data:{
		name:'张三',
		pwd:'123233',
		sex:'famale',
		hobby:['eat','sleep'],
		address:'Beijing'

	},
	methods:{
		//methods
		del:function(item){
			this.data.splice(this.data.indexOf(item),1);
		}
	}
});
```

7.

```javascript
<a :class="{visible:isShow"}></a>	
Vue可以用来控制class等visible，isShow=true,
```


## 计算属性

!!询问老师，计算属性:methods和computed和watched之间的区别及定义，用法
mutations、getters


## Class与style绑定

```javascript
//如果isActive为真则div的class为active
<div v-bind:class="{ active: isActive }"></div>

//批量处理class:isActive为真添加active，hasEroor为真添加text-danger
<div class="static"
     v-bind:class="{ active: isActive, 'text-danger': hasError }">
</div>

```


