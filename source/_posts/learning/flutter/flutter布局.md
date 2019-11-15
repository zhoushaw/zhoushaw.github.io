---
title: flutter常用布局
date: 2019-10-23 8:07:12
tags: flutter
categories: flutter
---


<div><!-- more--></div>


## Flutter 布局 Widget

单个属性的`Widget`是`child`,多个属性的`Widget`是`children`

> 单子Widget


Center 就是 单子Widget 的布局，它的 子Widget 属性是`child`


```
Center(
     child: Text(content),
)
```

> 多个Widget

```
Column(
    children: <Widget>[
        Text(content),
        Text(content),
        ...
    ]
)
```

## 布局方式


> 布局 Widget 还可以按照为子元素排布的方式分为：

* 弹性布局Widget
* 线性布局Widget
* 流式布局Widget
* 层叠布局Widget

## 弹性布局

详细属性请看：[flutter flex属性](https://juejin.im/book/5c5423ef6fb9a049cd54a213/section/5c7d6035f265da2da8359559)

flutter的弹性布局 类似于 CSS 的 `Flexbox`


通过`Flex`控件来实现

> 控件属性：

* direction 主轴方向
    * Axis.horizontal 
    * Axis.vertical 
* mainAxisAlignment 主轴排列方式
* crossAxisAlignment 交叉轴排列方式

## Flutter布局Widget

Row：水平方向的线性布局
Column：垂直方向的线性布局


```
Row(
  children: <Widget>[
    Text("Hello Flutter"),
    Image.asset(
      "images/flutter.png",
      width: 200,
    )
  ],
)
```

