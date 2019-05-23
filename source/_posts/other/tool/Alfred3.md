
---
title: alfred工具
date: 2019-03-1 2:44:53
tags: alfred
categories: tool
---

<div><!-- more--></div>

## 下载破解版

[文章地址](https://www.jianshu.com/p/5b3f98b1f7b6)

## 功能使用

[掘金地址](https://juejin.im/post/5b0e99436fb9a009e405dbb6)

## web搜索设置



* 百度:https://www.baidu.com/s?ie=utf-8&f=8&wd={query}
* stackoverflow:http://www.stackoverflow.com/search?q={query}
* githubUser:https://github.com/{query}
* githubSearch:https://github.com/search?utf8=%E2%9C%93&q={query}
* MDN:https://developer.mozilla.org/zh-CN/search?q={query}
* juejin: https://juejin.im/search?query={query}

## alfred集成iterm2


```
on alfred_script(q)
	if application "iTerm" is running or application "iTerm" is running then
		run script "
			on run {q}
				tell application \":Applications:iTerm.app\"
					activate
					try
						select first window
						set onlywindow to false
					on error
						create window with default profile
						select first window
						set onlywindow to true
					end try
					tell current session of the first window
						if onlywindow is false then
							tell split vertically with default profile
								write text q
							end tell
						end if
					end tell
				end tell
			end run
		" with parameters {q}
	else
		run script "
			on run {q}
				tell application \":Applications:iTerm.app\"
					activate
					try
						select first window
					on error
						create window with default profile
						select first window
					end try
					tell the first window
						tell current session to write text q
					end tell
				end tell
			end run
		" with parameters {q}
	end if
end alfred_script
```

## workflows

> 有道

https://github.com/kaiye/workflows-youdao/

## 修复alfred工作流错误


* [fixum修复工具下载](https://github.com/deanishe/alfred-fixum/releases/tag/v0.8)

* 导入`Fixum-0.8.alfredworkflow`修复工具
* 打开alfred快捷搜索，输入`fixum`,选择`fix workflows`

