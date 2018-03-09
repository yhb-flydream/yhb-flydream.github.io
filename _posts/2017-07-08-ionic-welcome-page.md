---
layout: post
title: App首次启动滑动欢迎界面
categories: ionic
description: 一款好的App在首次进入的时候都会有一个滑动的欢迎界面
keywords: js, ionic, cordova, hybird, welcome
---


#### App在第一次启动时都有一个欢迎界面，通常是几个单页面或者带动画的单页面滑动到最后一页有个启动的按钮
![](http://upload-images.jianshu.io/upload_images/4263048-7d9aae0c349dac6a.gif?imageMogr2/auto-orient/strip)

```
<ion-content padding>
    <ion-list>
 <ion-slides class="banner base-width" pager="true">
            <ion-slide>
                ![](assets/img/guide1.png)
            </ion-slide>
            <ion-slide>
                ![](assets/img/guide2.png)
            </ion-slide>
            <ion-slide>
                ![](assets/img/guide3.png)
            </ion-slide>
            <ion-slide>
                ![](assets/img/guide4.png)
            </ion-slide>
        </ion-slides>
    </ion-list>
</ion-content>
```
参考地址：
这里判断是否是第一次开启app采用的是native的storage组件，第一次启动会写入storage一个变量firstIn,下次启动时如果读取到这个变量则直接跳过欢迎页，注意ionic2开始storage默认使用的是IndexedDB，而不是LocalStorage
