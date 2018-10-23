---
title: better-scroll
date: 2018-01-20 14:52:35
tags: plugin
categories: learning
---


## 引言

在实际工作中我们常常遇到，二级联动的需求。通常是菜单栏和内容区域联级，切换菜单栏，内容区域滚动到与菜单栏关联的位置，滚动内容区域，菜单栏自动滚动切换到与内容关联的位置，而这种需求在实际工作中是非常常见的。

<div><!-- more--></div>

## 基础css知识

> 在了解使用better-scroll之前我们需要先来复习一下css基础知识

在web应用开发过程中，我们常常需要处理滚动条的问题。pc端页面，在网页打开后，都要求不出现滚动条以便增强用户体验(窗口最大化时)，而在移动端应用中出现横向滚动条会带来非常糟糕的用户体验

滚动条何时会出现呢？
<pre>
1.内容区域超过窗口大小，并且``内容区``域没有设置overflow: hidden属性(默认overflow: auto;)
2.盒子区域设置了overflow: scroll;``或``overflow: auto;内容超过盒子大小
3.当然也可以限定横向还是纵向，overflow-x、overflow-y属性
</pre>

## better-scroll

案例来自，饿了么移动端web实战中，菜单栏与内容区，联级。主要是vue中的实际应用
最终效果:
<image src="https://sf.dankal.cn/tmp/wxb6cbb81471348fec.o6zAJszA0KOosUhoTLKll8Q2-ufA.808b7860eef1b3ff0aaeb664e046b073.gif" alt="" style="height:400px;" />


> 起步

```javascript
cnpm install better-scroll --save (淘宝镜像使用,不了解的自行google)
或
npm intall better-scroll --save
```

> 引入模块，初始化要滚动的结点

结构部分:

```html
    <div class="menu-wrapper" ref="menuWrapper">
      <ul>
        <li class="menu-item"  :class="{'current':currentIndex === index}" v-for="(item,index) in goods" @click="selectMenu(index, $event)">
          <span>
          	....
          </span>
        </li>
      </ul>
    </div>
```

> 初始化BScroll

```javascript

import BScroll from 'better-scroll'

//其中的$nextTick只有在DOM加载完成后才会执行，初始化需要使用better-scroll的组件
this.$nextTick(()=>{
  this._initScroll();
  this._calculateHeight();
})

```

```javascript

_initScroll() {
	// 使用$refs获取到vue中的dom结点,BScroll第一个参数是要初始化的结点，第二个参数要初始化附带的参数
  this.menuScroll = new BScroll(this.$refs.menuWrapper,{
    click: true
  })
  this.foodScroll = new BScroll(this.$refs.foodWrapper,{
    click: true,
  	//探针作用，实时监测滚动位置
    probeType: 3
  })
  
  //初始化监听事件，当food部分滚动时，触发回调事件,将当前滚动的位置存入scrolly
  this.foodScroll.on('scroll', (pos) => {
    this.scrolly = Math.abs(Math.round(pos.y));
  });
},

_calculateHeight() {
	//获取food标签内所有food-list-hook类名的标签，将其所有位置所在的高度存起来，计算一个个高度相加算出当前结点所在位置
  let foodList = this.$refs.foodWrapper.getElementsByClassName('food-list-hook');
  let height = 0;
  this.listHeight.push(height);
  for(let i =0;i<foodList.length;i++){
    let item = foodList[i];
    height += item.clientHeight;
    this.listHeight.push(height);
  }
}

```

> 初始化事件

```javascript
    selectMenu(index, event){
    	//点击食物菜单后，传入点击的菜单index，通过该元素的位置获取初始化好的值，传入BScroll实例对象中
      let foodList = this.$refs.foodWrapper.getElementsByClassName('food-list-hook');
      let el = foodList[index];
      this.foodScroll.scrollToElement(el,300);
    }
```


