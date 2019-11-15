---
title: flutter盒模型
date: 2019-10-23 8:07:12
tags: flutter
categories: flutter
---


<div><!-- more--></div>


## BoxConstraint分类


* Tightly Constraints（严格约束）
* Loose Constraints（松散约束）
* Bounded Constraints（有界约束）
* Unbounded Constraints（无界约束）
* Infinite Constraints（无限约束）


## Tightly Constraints（严格约束）

> 特点：

* 盒模型的宽高最大值最小值相等
* 有无子节点，盒模型宽高不受影响


> 使用方式：


```
BoxConstraints.tight(Size(100, 100))
```

```
body: Container(
    constraints: BoxConstraints.tight(Size(100, 100)), //添加 Tightly Constraints
    color: Colors.red,
    child: Text(
      "HelloWorld",
      style: TextStyle(background: paint),
    ))));
```



## Loose Constraints（松散约束）


> 特点：

* 盒模型的宽或高其中某一最小值为0
* 子节点不超过盒模型的宽高时，盒模型的大小与子节点相等
* 没有子节点时，盒模型的宽高为最大值


> 使用方式：


```
BoxConstraints.loose(Size(width, height))
```

```
body: Container(
        constraints: BoxConstraints.loose(Size(100, 100)), //添加 Loose Constraints
        color: Colors.red,
        child: Text(
          "HelloWorld",
          style: TextStyle(background: paint),
        ))));
```

### 最大值是是 Infinite(无限值)

特点：

* 继承了松散约束，且没有子节点时，盒子的宽高为屏幕宽高

> 无限值的松散约束：


```
BoxConstraints.tightFor()
```

> 代码使用


```
body: Container(
    constraints: BoxConstraints.tightFor(), //添加 Loose Constraints
    color: Colors.red,
    child: Text(
      "HelloWorld",
      style: TextStyle(background: paint),
    ))));
```


## Bounded Constraints（有界约束）


> 特点：

* 盒模型的宽或高其中一值未固定值时
* 有无子节点，盒模型宽高为最大值


> 使用方式：


```
BoxConstraints(minWidth,maxWidth,minHeight,maxHeight)
```

```
body: Container(
    constraints: BoxConstraints(minWidth: 100,maxWidth: 300,minHeight: 0,maxHeight: 300), //添加 Bounded Constraints
    color: Colors.red,
    child: Text(
      "HelloWorld",
      style: TextStyle(background: paint),
    ))));
```

### Unbounded Constraints（无界约束）


> 特点：

* 当盒模型的宽或高一值为Infinite(无限值) 时
* 子元素小于盒模型时，按最小宽高展示
* 没有子元素，宽高为屏幕宽高

> 使用：


```
BoxConstraints(minWidth: 10,maxWidth: double.infinity,minHeight: 100,maxHeight: double.infinity)
```


## Infinite Constraints（无限约束）

> 特点：

* 宽高最小值和最大值都是 Infinite(无限值)
* 不受子元素影响宽高
* 展示宽高屏幕宽高

> 使用：

```
BoxConstraints.expand()
```


```
body: Container(
    constraints: BoxConstraints.expand(), //添加 Infinite Constraints
    color: Colors.red,
    child: Text(
      "HelloWorld",
      style: TextStyle(background: paint),
    ))));
```

