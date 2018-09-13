---
layout: post
title: ionic开发中遇到的坑
categories: ionic
description: 记录一下ionic开发中遇到的坑
keywords: js, ionic, cordova, hybird, bug
---


### 1.打包的时候出错：

Execution failed for task ':transformClassesWithDexForDebug
![bug1](/images/posts/ionic/ionic-bug1.png)

##### 解决办法：

删除F:\web\KmfApp2.0_up\upupup\platforms\android\libs中的android_support_v4.jar的jar包

[参考：](http://blog.csdn.net/shunzi1046/article/details/51279932)

#### 2.错误如下：找不到已经安装的 Gradle 编译版本

注：当时版本是cordova7.0.1  安卓 <engine name='android' spec='^6.2.3'>,好像和这个也有关系因为换着6.1.1之后错误不一样了，反正记录一下
![bug2](/images/posts/ionic/ionic-bug2.png)


亲测，下面方法有效，感人
![bug2-close](/images/posts/ionic/ionic-bug2-close.png)


```
else {

//OK, let's try to check for Gradle!

var sdkDir = process.env['ANDROID_HOME'];

return path.join(sdkDir, 'tools', 'templates', 'gradle', 'wrapper', 'gradlew');

}
```

[参考：](https://stackoverflow.com/questions/43356833/cordova-android-requirements-failed-could-not-find-an-installed-version-of-gra)

#### 3.ionic2.2.1中页面默认返回上一页会有短暂的白屏，通过修改app配置来解决页面跳转动画


app.module.ts中修改配置
```
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
```


#### 4.使用ionic3新特性懒加载的时候代码没有出错，但是却报错can't find 新建的module


 Google了一下，好像是cnpm的锅,我用重新用npm测试了一下,没有问题了,看来真是cnpm的锅,论翻墙的重要性！
