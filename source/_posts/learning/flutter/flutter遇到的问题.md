---
title: flutter开发、安装问题合集
date: 2019-10-23 8:07:12
tags: flutter
categories: flutter
---


<div><!-- more--></div>

## 基本环境问题


> `CocoaPods installed but not initialised`问题

[flutter CocaPods not initialised](https://github.com/flutter/flutter/issues/41291)

```
sudo gem uninstall cocoapods
sudo gem install cocoapods -v 1.7.5
pod setup
```


[真机调试用flutter开发ios应用时出现的问题的总结](https://blog.iw3c.com/archive/1147)


app创建名称必须和`Bundle Identifier`一致

> Device doesn't support wireless sync. AMDeviceStartSe


```
cd ~/Desktop
wget https://raw.githubusercontent.com/kangwang1988/kangwang1988.github.io/master/others/ios-deploy
chmod +x ios-deploy
mv ios-deploy /usr/local/bin
```

