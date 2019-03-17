---
title: css常见布局
date: 2018-01-15 11:07:35
tags: css
categories: css
---

<div><!-- more--></div>


## sticky布局

> 在网页设计中，**Sticky footers**设计是最古老和最常见的效果之一，大多数人都曾经经历过。它可以概括如下:如果页面内容不够长的时候，页脚块粘贴在视窗底部；如果内容足够长时，页脚块会被内容向下推送，我们看到的效果就如下面两张图这样。这种效果基本是无处不在的，很受欢迎。

<div style="display:flex;justify-content:space-between;align-items:center;">
    <img src="https://www.w3cplus.com/sites/default/files/blogs/2015/1507/css-secrets-7-21.png" style="display:inline-block;width:200px;border:none;">
    <img src="https://www.w3cplus.com/sites/default/files/blogs/2015/1507/css-secrets-7-22.png" style="display:inline-block;width:200px;border:none;">
</div>


> 解决方案


**1.html部分**

```html
<div class="box">
	<div class="content">content</div>
	<div class="footer"></div>
</div>

```


> 方案一

```css
.box{
	min-height: 100%;
}
.content{
	padding-bottom: 100px;
}
.footer{
	height: 100px;
	margin-top: 100px;
}
```

> 方案二

```css

.content{
	min-heigt: calc(100vh-100px);
}
.footer{
	height: 100px;
}
```

## transition and fixed

父元素使用了transition，子元素的position: fixed；会降级为absolute

