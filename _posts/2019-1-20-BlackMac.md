---
layout: post
title: NUC8ibeh黑苹果
---

###解决开机粉屏的问题
```sh
1、终端打开，运行
ioreg -l | grep IODisplayEDID
只复制<>里的一长串内容，提取你显示器特有的edid
2、Clover Configurator程序，Graphics下，粘贴上面的内容，复选 inject edid保存
3、rebuild kextcache 重启。
刚用家里的Sharp电视1080p试了，完美解决开机闪一下粉屏的问题。
```
