---
title: sass常用语法
date: 2018-01-14 3:07:33
tags: css
categories: sass
---



## 引言

**前端工程化**，越来越被人们提及，不断涌出的前端框架，各种插件使前端变得简单同时也复杂了。
作为前端的主要部分，css描述语言，主要用于编写样式，在复杂项目的开发中，由于css没有``模块化``的概念，大量的css编写，在前期开发过程中大量的代码冗余，而且后期维护将会十分困难。本文将介绍的是sass，**函数**式编程编写css

<div><!-- more--></div>

## mixin宏css函数式编程

```python
@mixin bg-image($url){
    background-image: url("/static/"+ $url + "@2x.png")
}
```

> mixin宏定义，函数式css编写

<dl>
    <dt>@mixin:</dt>
    <dd> 类似于javascript中的function 声明函数，</dd>
    <dt>bg-image:</dt>
    <dd>名为bg-image的函数</dd>
    <dt>$url:</dt>
    <dd>
        在sass中，变量的定义方式使用$符号表示<br/>例:$url www.baidu.com
    </dd>
</dl>

> include将mixin宏定义的函数使用

```javascript
.brand{
    @include bg-image('img/brand');
}
```

<dl>
    <dt>@include:</dt>
    <dd>使用mixin宏定义的函数，后面跟上函数名和参数</dd>
</dl>

## css遍历器each

> 使用each遍历器将会在实际工作中减少大量的类名定义工作

``例如``:

```html

 <span class="icon" :class="classMap[seller.supports[0].type]"></span>
```

```javascript
this.classMap = ["decrease","discount","special","invoice","guarantee"]
```

```css
$goodsType: decrease discount special invoice guarantee;

@each $types in $goodsType{
    &.#{$types}{
        @include bg-image('img/'+$types+'_1');
    }
}
```


<dl>
    <dt>$goodsType:</dt>
    <dd>定义数组变量名为goodsType，参数decrease,discoutn...</dd>
    <dt>@each:</dt>
    <dd>其中$types in $goodsType相当于javascript中的for i in item</dd>
    <dt>#{$types}</dt>
    <dd>一般我们定义的变量都为属性值，可直接使用，但是如果变量作为属性或在某些特殊情况下等则必须要以 #{$variables}形式使用。</dd>
</dl>

## 条件判断

> 实际项目中常常需要通过类名修改内容大小，造成大量的css冗余，通过遍历器和条件判断可以很好地解决

```css
$starTypes: 48 36 24;

@each $type in $starTypes
    @if($type==48){
        width: 40px;
        height: 40px;
    }@else if($type==36){
        width: 30px;
        height: 30px;
    }@else{
        width: 20px;
        height: 20px;
    }
}
```