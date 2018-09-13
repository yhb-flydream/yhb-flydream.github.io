---
layout: post
title: ionic页面周期
categories: ionic
description: ionic页面周期钩子函数
keywords: js, ionic, cordova, hybird, hooks
---

页面的生命周期钩子

Angular

钩子目的和时机

[官方文档：](https://angular.cn/docs/ts/latest/guide/lifecycle-hooks.html)

![image](/images/posts/ionic/ng-page-hooks.png)


使用：export class demo  implementsOnInit,OnDestroy{}



ionic2/3的生命周期钩子：

官方文档地址在这里。

[ionic](http://ionicframework.com/docs/api/navigation/NavController/)
![image](/images/posts/ionic/ionic-page-hooks.png)

页面周期
事件名称事件说明

ionViewLoaded页面加载完毕触发。该事件发生在页面被创建成 DOM 的时候，且仅仅执行一次。如果页面被缓存（Ionic默认是缓存的）就不会再次触发该事件。该事件中可以放置初始化页面的一些事件。

ionViewWillEnter即将进入一个页面变成当前激活页面的时候执行的事件。

ionViewDidEnter进入了一个页面且变成了当前的激活页面，该事件不管是第一次进入还是缓存后进入都将执行。

ionViewWillLeave将要离开了该页面之后变成了不是当前激活页面的时候执行的事件。

ionViewDidLeave在页面完成了离开该页面并变成了不是当前激活页面的时候执行的事件。

ionViewWillUnload在页面销毁和页面中有元素移除之前执行的事件。

ionViewDidUnload在页面销毁和页面中有元素移除之后执行的事件。

作用：

利用生命周期来做权限：

比如我自己的项目中用到的，禁止页面后退（业务需要，必须向下进行）

[GitHub项目](https://github.com/xiedajian/ipvpKmfApp2.0/blob/master/src/pages/TrackingModule/tracking/tracking.ts)
