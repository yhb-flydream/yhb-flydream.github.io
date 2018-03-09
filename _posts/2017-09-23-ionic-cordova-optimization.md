---
layout: post
title: cordova内核优化
categories: ionic
description: cordova内核优化,处理cordova安卓手机兼容性问题
keywords: js, ionic, cordova, hybird, bug
---


### 问题：
从研发cordova混编App开发开始，不同安卓版本手机上的兼容性问题就困扰着研发的童鞋们。Cordova使用的web引擎是手机系统自带的WebView，兼容性问题很多都是安卓不同版本的系统webview的差异导致的，有可能是安卓系统的问题，也有可能是手机厂商修改webkit带来的问题，这些问题从前端技术层面是很难解决的，修改和测试成本都非常高。

### 浏览器内核介绍
如果细分的话，目前全球仅有四个独立的浏览器内核，分别为微软IE的Trident、网景最初研发后卖给Mozilla基金会并演化成火狐的Gecko、KDE的开源内核Webkit以及Opera(欧朋)的Presto。其中，Presto是历史最悠久的内核。

### 整体归纳下几种内核的优缺点吧：
1.Trident:因为在早期IE占有大量的市场份额，所以以前有很多网页是根据这个Trident的标准来编写的，但是实际上这个内核对真正的网页标准支持不是很好，同时存在许多安全Bug。
2.Gecko:优点就是功能强大、丰富，可以支持很多复杂网页效果和浏览器扩展接口，缺点是消耗很多的资源，比如内存。
3.Webkit:优点就是Webkit拥有清晰的源码结构、极快的渲染速度，缺点是对网页代码的兼容性较低，会使一些编写不标准的网页无法正确显示。
4.Presto：Presto内核被称为公认的浏览网页速度最快的内核，同时也是处理JS脚本最兼容的内核，能在Windows、Mac及Linux操作系统下完美运行。

### 移动端浏览器
目前微软的Trident在移动终端上主要为WP系统内置浏览器，Webkit内核的适用范围则较为广泛，Android原生浏览器、苹果的Safari、谷歌的Chrome(Android4.0使用)都是基于Webkit开源内核开发的。
目前，移动设备浏览器上常用的内核有Webkit，Blink，Trident，Gecko等，其中iPhone和iPad等苹果iOS平台主要是WebKit，Android 4.4之前的Android系统浏览器内核是WebKit，Android4.4系统浏览器切换到了Chromium(内核是Webkit的分支Blink)，Windows Phone 8系统浏览器内核是Trident。

### 从实际情况出发：
对于Android手机而言，使用率最高的就是Webkit内核，我们看到很多手机浏览器厂商都宣称有着自主内核，比如手机UC就号称采用了U3内核、而华为也经常标榜自己的天天浏览器采用了T9内核，事实上，他们都是基于开源内核Webkit进行二次开发的，并不是完全的自主内核。
而在iOS以及WP7平台上，由于系统封闭，不允许除系统自带浏览器内核以外的浏览器内核进入，因此各家浏览器的开发均为在Safari或者IE内核的基础上进行二次开发，优化功能和自制UI。

微信6.1版本以上的android用户，都是使用的QQ浏览器的X5内核。5.4-6.1之间的版本，若用户安装了QQ浏览器就是使用的X5内核，若用户未安装浏览器，使用的是系统内核。
QQ浏览器的X5内核基于 Blink内核


### cordova应用内核
Cordova(PhoneGap)，作为第三方的HTML5应用开发框架工具的代表，极大促进了HTML5应用的发展。它提供了方便的跨平台应用打包/发布服务、实用的API、灵活的扩展机制、以及积累下来的丰富的第三方API实现。然而Cordova使用的web引擎是系统的WebView。如果开发者正在使用Cordova并且渴望更好的性能和更新的功能，如WebGL，更换内核是个不错的选择。


### 终极解决方案
通过使用统一webkit内核的大招来解决，目前有2个方案可选，使用Crosswalk内核 或 腾讯浏览服务X5内核。

##### 1.Crosswalk内核
熟悉Cordova生态圈的朋友可能听说过Crosswalk，[Crosswalk]是Intel维护的Webkit开源项目，可以通过插件安装命令安装，是一个很好的选择。
```
$ cordova plugin add cordova-plugin-crosswalk-webview
```
[Crosswalk](https://crosswalk-project.org/)支持开发者在Cordova中用Crosswalk替换原生的Android WebView，并将两者完美的融合。当然，它仍然支持Crodova的扩展机制，不过如果web应用对扩展的性能要求较高， 采用Crosswalk自带的扩展机制是更好的选择。
它的缺点就是太大了，集成后apk会增加20M，在安装后会解压缩到100M+，首次安装还需要解压缩时间，造成的用户体验甚是不好。一系列的问题就跟着来了，解压缩需要时间，如果操作快了，或者CPU性能不行，打开Hybrid页面就会出现Application Error等问题。还有些机型如魅族，安装Crosswalk后，就会Crash，让研发的童鞋更是摸不着头脑。

不过在我做过的两个app中，确实是通过Crosswalk解决了一些魅族和华为的问题，也出现过报错App打开失败（只出现过一次）

##### 2.腾讯浏览服务X5内核。

[腾讯浏览服务X5](http://x5.tencent.com/index),它是直接使用微信/手机QQ/空间的X5浏览器内核的，SDK只有250k，因此可以放心使用。鉴于这几个产品国内广泛的装机量，用户覆盖方面不用担心，如果微信/手机QQ/空间都没有安装，会自动降级到系统浏览器内核，或提示用户安装X5内核。

X5SDK是通过调用微信/手机QQ/空间的X5内核，解决系统webview兼容性差、加载速度慢、功能缺陷等问题，开发接入便捷，大小只有253K，仅需几行代码，即可解决一切令开发者们头疼的问题，为用户提供最优秀的浏览体验。

同时，QQ浏览器团队还将持续更新和优化X5内核，持续优化功能，并保证兼容各种web新特性。
其相对于系统webview，具有下述明显优势：
1) 速度快：相比系统webView的网页加载速度有近30%的提升。
2) 省流量：云端优化技术使流量节省20%
3) 更安全：24小时安全问题解决机制
4) 更稳定：经过亿级用户的使用考验，CRASH率0.15%
5) 集成强大的视频播放器，支持各种视频格式直接打开
6) 适屏排版、字体设置等浏览增强功能的提供
7) Html5更完整支持。
8) 无系统内核的碎片化问题，更少的兼容性问题

[X5内核支持Cordova啦](http://bbs.mb.qq.com/thread-1945157-1-1.html)

Add this plugin
```
$ cordova plugin add cordova-plugin-x5-webview
````

Build
```
$ cordova build android
```