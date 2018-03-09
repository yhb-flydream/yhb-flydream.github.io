---
layout: post
title: ionic修改app图标和启动页面
categories: ionic
description: ionic修改app图标和启动页面
keywords: js, ionic, cordova, hybird, hooks
---

### 自定义图标和启动页
在执行新建项目命令ionic start demo时，会自动创建一个resources文件下，用于存放app的图标和启动页。如图是创建的默认的图标和启动页

![image.png](http://upload-images.jianshu.io/upload_images/4263048-32f13fcad7a7fbe9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
 
在这个文件下下，icon.png和splash.png分别代表着图标和启动页的原始图标。
以安卓（android文件）为例，就是根据icon.png和splash.png来自动剪裁好的，各个尺寸的图标和启动页，已适应各个不同分辨率的手机。
自定义图标和启动页只需要替换掉默认的 icon.png和splash.png，（最好尺寸一样）
然后执行下面命令
    ionic resources			（可生成不同分辨率手机所需要的icon和splash）
    ionic resources --icon			（只生成图标）
    ionic resources --splash			（只生成启动画面）
就可以生成自动以的图标和启动页，如图：

![image.png](http://upload-images.jianshu.io/upload_images/4263048-7aaf4fffe11ea1f6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


