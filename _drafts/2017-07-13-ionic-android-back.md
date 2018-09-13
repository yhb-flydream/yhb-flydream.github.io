---
layout: post
title: ionic注册安卓物理返回键
categories: ionic
description: ionic注册安卓物理返回键
keywords: js, ionic, cordova, hybird
---

#### 前言：
在网上找了一些参考的资料，但是和他们情况不太一样的，他们的app根入口直接是tabs，但是我们项目中app的根入口可能会有四个，这些页面 也是不能后退的，所以自己改写了一个

有双击退出 或者是 app最小化后台运行 两种方案
话不多说，代码如下：
```
 //注册安卓物理返回键
    registerBackButtonAction() {
        this.platform.registerBackButtonAction(() => {
            //如果有弹窗或loading，返回键什么也不做
            let activeLoading = this.ionicApp._loadingPortal.getActive();
            let activeOverlay = this.ionicApp._overlayPortal.getActive();
            if (activeLoading || activeOverlay) {
                return;
            }
            //处理modal
            let activeModal = this.ionicApp._modalPortal.getActive();
            if (activeModal) {
                activeModal.dismiss().catch(() => {
                });
                activeModal.onDidDismiss(() => {
                });
                return;
            }
            // 返回当前活动页面的视图控制器
            let activeVC = this.nav.getActive();
            let page = activeVC.instance;
            //如果当前页面不是tabs页面
            if (!(page instanceof TabsPage)) {
                // if (page instanceof LoginComponent || page instanceof TodayScheduleComponent || !this.nav.canGoBack()) {
                //     return this.showExit();
                // }
                return this.appMinimize.minimize();
                // return this.nav.pop();
            }
            let tabs = page.tabs;
            // 返回tabs当前选中的选项卡
            let activeNav = tabs.getSelected();
            //双击退出
            // return activeNav.canGoBack() ? activeNav.pop() : this.showExit();
            //最小化app
            return activeNav.canGoBack() ? activeNav.pop() :  this.appMinimize.minimize();
        }, 1);
    }

    //双击退出App提示框
    showExit() {
        if (this.backButtonPressed) { //当触发标志为true时，即2秒内双击返回按键则退出APP
            this.platform.exitApp();
        } else {
            this.toastCtrl.create({
                message: '再按一次退出应用',
                duration: 2000,
                position: 'top'
            }).present();
            this.backButtonPressed = true;
            setTimeout(() => this.backButtonPressed = false, 2000);//2秒内没有再次点击返回则将触发标志标记为false
        }
    }

```

本人github传送门，欢迎star：
[GitHub](https://github.com/xiedajian/ipvpKmfApp2.0/blob/master/src/app/app.component.ts)
参考：https://dpary.github.io/2016/12/19/
参考：http://www.jianshu.com/p/6aa5a8318092
