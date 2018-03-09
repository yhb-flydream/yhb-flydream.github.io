---
layout: post
title: ionic项目下面hooks文件夹介绍
categories: ionic
description: hooks文件夹作用介绍
keywords: hook, ionic, cordova, hybird
---

在使用ionic做项目的时候，发现 项目存在一个hooks文件夹，查找相关资料做个简单记录
[官方文档：](http://cordova.apache.org/docs/en/7.x/guide/appdev/hooks/index.html)

###介绍：
Cordova Hooks代表特殊脚本，可以由应用程序和插件开发人员添加，甚至可以通过自己的构建系统来自定义cordova命令。

Cordova挂钩允许您对cordova命令执行特殊活动。例如，您可能有一个自定义工具来检查您的JavaScript文件中的代码格式。而且，您希望在每次构建之前运行此工具。在这种情况下，您可以使用“before_build”钩子，并指示cordova运行时间运行在每次构建之前调用的自定义工具。

钩可能与你的应用程序的活动，如如before_build， after_build等。或者，他们可能与你的应用程序的插件。例如，挂钩等before_plugin_add，after_plugin_add等适用于插件相关的活动。这些钩子可以与应用程序中的所有插件相关联，也可以仅与一个插件相关联。

Cordova支持以下钩类型：
![这里写图片描述](http://upload-images.jianshu.io/upload_images/4263048-62d21f035061dd54?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)![这里写图片描述](http://upload-images.jianshu.io/upload_images/4263048-eeca5566d49cbad5?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)![这里写图片描述](http://upload-images.jianshu.io/upload_images/4263048-ae3a1707571cc4de?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)![这里写图片描述](http://upload-images.jianshu.io/upload_images/4263048-7da2f76bfdeef35d?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)