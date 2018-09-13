---
layout: post
title: ionic2/3全局设置配置
categories: ionic
description: ionic3没有全局变量，怎么自定义全局变量
keywords: js, ionic, cordova, hybird
---

##### [官方文档传送门：](http://ionicframework.com/docs/api/config/Config/)         

![image](/images/posts/ionic/global-set-config.png)

选项表
项目中实际运行：

在ionic2.2.1框架版本中，发现默认的页面返回上一页会有个短暂的白屏的问题，通过修改页面切换配置解决

```
    imports: [
        BrowserModule,
        HttpModule,
        // PipesModule,
        IonicStorageModule.forRoot(),
        IonicModule.forRoot(MyApp, {
            tabsHideOnSubPages: true,
            //backButtonText: '返回',
            backButtonIcon: 'arrow-back',
            iconMode: 'ios',
            mode: 'ios',
            pageTransition: 'md-transition',
            pageTransitionDelay: 16,
            popoverEnter: 'picker-slide-in',
            popoverLeave: 'picker-slide-out',
            modalEnter: 'modal-slide-in',
            modalLeave: 'modal-slide-out',
        })
    ],
```
设置配置
