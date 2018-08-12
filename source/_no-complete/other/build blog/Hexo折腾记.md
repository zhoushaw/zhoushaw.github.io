---
title: Hexo折腾记
date: 2017-04-29 19:34:04
tags: hexo
categories: other
---
 <div><!--more--></div>

## 搭建hexo
<a href="https://xuanwo.org/2015/03/26/hexo-intor/">hexo搭建参考文章</a>
搭建要使用ssh秘钥链接
## 高亮代码显示
语法格式
``` c
(```c)
int main(){
  return main();

}
 (```)
```

这样的写法才能显示出高亮的代码，并且附带行数，给hexo主题去解析去掉括号


## 增加hexo，热更新

```javascript

npm install hexo-browsersync --save

```
[browersync插件](https://github.com/hexojs/hexo-browsersync)


### 站点文件_config.yml中配置 

``` javascript
	highlight:
	  enable: true
	  line_number: true
	  auto_detect: true
	  tab_replace:

```

### themes文件_config.yml中配置 

``` javascript

	highlight_theme: night eighties//看主题提供了什么样的格式

```
这样子就完成了配置

## hexo主题默认a标签带下划线 ##

因为hexo默认的是a标签带border-bottom：black样式，所以在文章中要使用border-bottom： none；样式来清除自带的属性

blog\themes\next\source\css\_common\components\sidebar\sidebar.sty
中可以设置友链接的下划线

## 为Hexo Next主题添加哈林摇特效 ##

<a href="http://www.iamlj.com/2016/08/add-special-effect-harlem-shake-for-hexo/">添加哈林摇特效,原作地址</a>

## 博客的搜索插件 ##

可以去next官方文档查看

## git，部署常用命令 ##

```c
	
	npm install hexo -g #安装  
	npm update hexo -g #升级  
	hexo init #初始化
	
	hexo n "我的博客" == hexo new "我的博客" #新建文章
	hexo p == hexo publish
	hexo g == hexo generate#生成
	hexo s == hexo server #启动服务预览
	hexo d == hexo deploy#部署

````

服务器
```c
	hexo server #Hexo 会监视文件变动并自动更新，您无须重启服务器。
	hexo server -s #静态模式
	hexo server -p 5000 #更改端口
	hexo server -i 192.168.1.1 #自定义 IP
	
	hexo clean #清除缓存 网页正常情况下可以忽略此条命令
	hexo g #生成静态网页
	hexo d #开始部署
```
## RSS订阅 ##

安装RSS插件

npm install hexo-generator-feed --save
开启RSS功能

编辑hexo/_config.yml，添加如下代码：

rss: /atom.xml #rss地址  默认即可

## 使用locovpn无法上传博客

上传博客时，关闭vpn

## 博客出问题时

hexo clean 

hexo init /*初始化数据*/

hexo g

hexo d -g



