---
title: 微信小程序开发
date: 2017-09-26 1:36:18
tags: wechat
categories: wechat
---


<span><!--more--></span>

## 事件处理

bindtouchmove:监听拖拽事件，回调函数的参数可以访问到，物体的位置等信息，
通过提供的pageX，clientX等参数控制物体位置，实现拖拽


## 动画

```javascript

<view animation="{{animationData}}" style="background:red;height:100rpx;width:100rpx"></view>

创建一个动画实例animation。调用实例的方法来描述动画。
最后通过动画实例的export方法导出动画数据传递给组件的animation属性。

//设置动画过程信息
var animation = wx.createAnimation({
  duration: 1000,
    timingFunction: 'ease',
})


animation.scale(2,2).rotate(45).step()

this.setData({
  animationData:animation.export()
})



```


## 小程序缺陷

> input 框问题
input 设置了placeholder之后，会出现层次问题
使用placeholder-class,并设置z-inde:0;

> 多层跳转

```javascript
	const Routeswitch= (router,success,error)=>{
	  
	  var app = getApp();
	  var canSwitch = app.globalData.Routeswitching;
	  if (canSwitch) {
	    app.globalData.Routeswitching = false;
	    wx.navigateTo({
	      url: router,
	      success:function(){
	        success?success():''
	      },
	      error: function(){
	        error?error():''
	      },
	      complete: function () {
	        setTimeout(function () {
	          app.globalData.Routeswitching = true;
	        }, 500);
	      }
	    })
	  }
	} 
```