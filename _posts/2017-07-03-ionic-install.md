---
layout: post
title: ionic环境搭建
categories: ionic
description: ionic环境搭建，新建项目入门教程
keywords: js, ionic, cordova, hybird
---

### 一.准备工作:
##### 下载安装	Node.js （npm依赖包）JDK （Java开发工具包，即Java Develop Kit）Android SDK  （用于android编译）

注：node.js  jdk  androidsdk需要加入环境变量path中

###### 1.1 安装node.js

测试是否安装成功

cmd输入 node -v

###### 1.2 安装jdk

安装jdk时会安装两次 一次是安装jdk 一次是安装jer 不要装在同一个文件夹下，会报错

建议放在同一个父目录java下，一个jar、一个jer文件夹

JRE： Java Runtime Environment

JDK：Java Development Kit

JRE顾名思义是java运行时环境，包含了java虚拟机，java基础类库。是使用java语言编写的程序运行所需要的软件环境，是提供给想运行java程序的用户使用的。

JDK顾名思义是java开发工具包，是程序员使用java语言编写java程序所需的开发工具包，是提供给程序员使用的。JDK包含了JRE，同时还包含了编译java源码的编译器javac，还包含了很多java程序调试和分析的工具：jconsole，jvisualvm等工具软件，还包含了java程序编写所需的文档和demo例子程序。

安装完成之后 配置环境变量
```

JAVA_HOME	D:\web\java\jdk  （指向jdk的安装目录）

path        %JAVA_HOME%\bin

                 %JAVA_HOME%\jre\bin
```                 

测试是否安装成功

cmd输入	java -version

###### 1.3 下载android_sdk

解压后运行 sdk-manager.exe 下载需要的工具

配置环境变量
```

ANDROID_HOME    D:\web\android-sdk

path        %ANDROID_HOME%\tools

                %ANDROID_HOME%\platform-tools
```

###### 1.4谷歌浏览器设置

桌面图标 -右击属性-快捷方式-目标

后面加入以下代码

--args --disable-web-security --user-data-dir

注：关于这个设置，是为了解决ionic项目在谷歌浏览器调试时js跨域。关于跨域，网上很多解决方法，服务端设置或者代理，但是因为ionic打包app之后再手机上运行是不存在跨域的问题的，只是在浏览器调试时跨域，属于只需要设置浏览器非安全模式就可以了，简单粗暴的方法。

#### 二.安装ionic，cordova

###### 2.1通过nodejs自带npm来管理项目的依赖包（关于npm的知识自行百度）

###### 安装命令：

npm install -g cordova ionic       //  -g代表全家安装

不够由于GFW，下载速度不忍直视，所以我们用npm淘宝镜像cnpm

npm install -g cnpm --registry=https://registry.npm.taobao.org

安装之后，以后可以用cnpm来代替npm命令使用

cnpm install -g ionic cordova

###### 其他常用命令

npm update -g cordova ionic    //更新

npm install -g ionic@latest  //安装最新版本ionic

npm install -g ionic@1.7    //安装特定版本ionic

npm install -g cordova@6.5    //安装特定版本cordova

npm uninstall cordova -g      //卸载

npm help    //查看全部命令

#### 三.新建项目

在安装最新版本ionic3.4.2之后，ionic v3CLI发生了一些变化：

[参照：](https://docs.google.com/document/d/1r8nTAaJ5hLIJ1DCwBozU-JGV480Du0xCMIg2dj3JRQo/edit#)
![image](/images/posts/ionic/ionic-CLI.png)

CLI
本次版本从ionic2.2.1升级到ionic3.3，CLI升级到3.4.0,

版本记录：
![image](/images/posts/ionic/ionic-version-info.png)

版本记录
###### 新建项目

ionic start myapp tabs|sidemenu|blank|super|tutorial

ionic serve

详情见[官方：](http://ionicframework.com/docs/intro/installation/)

浏览器调试查看      ionic serve

生成图标和启动页     ionic resources

添加平台     ionic cordova platform addandroid/ios

添加平台      ionic cordova platform removeandroid/ios

安装插件    ionic cordova plugin add XXX

移除插件    ionic cordova plugin remove XXX

打包（测试）    ionic cordova build android

ionic cordova build  android --release（正式包）

打包时加上--prod的优化启动速度，例如

ionic cordova  build  android --prod --release（正式包）



adb  cordova devices	（检测安卓手机连接） 

ionic cordova run android	（连接上手机运行） 

ionic cordova emulate android （模拟器运行）

ionic build android  //打包测试包

ionic build --release android  //打包正式包

###### 2.2如何用xcode 打包IONIC 项目（IPK）

将项目文件copy到MAC底下。运行终端，cd到项目所在文件夹，运行

ionic platform add ios

然后finder，在 platforms->ios->xxx.xcodeproj 打开项目

然后，将xcode的模拟器类型选成iOS Device

然后在XCODE 的菜单栏 选择 Product -- Archive ，会生成 xxx的Archive文件。

在窗口右侧的Submit to AppStore 按钮的下方，点击 Export...

###### 有三个选项

Save to IOS App Store Deployment

Save to Ad Hoc Deployment

Save for Enterprise Deployment

第一个是发布到APPStore

第二个临时打包，可以用来测试

第三个是发布成企业版本

选择证书等等，选择导出文件夹，导出

#### 三.apk签名

###### 3.1生成签名(.keystore)文件
```

keytool -genkey -v -keystore demo.keystore -alias demo.keystore -keyalg RSA -validity 20000
```

keytool是工具名称，

-genkey意味着执行的是生成数字证书操作，-v表示将生成证书的详细信息打印出来；

-keystore demo.keystore 证书的文件名；

-alias demo.keystore 表示证书的别名

-keyalg RSA 生成密钥文件所采用的算法；

-validity 20000 该数字证书的有效期；

输入后会让你回答关于你公司和地区的一些问题，这些回答一定要记住，以后更新apk的时候需要用到，最好截屏记录。

###### 3.2签名apk
```

jarsigner -verbose -keystore /yourpath/demo.keystore -signedjar demo_signed.apk demo.apk demo.keystore
```

jarsigner是工具名称，-verbose表示将签名过程中的详细信息打印出来；

-keystore /yourpath/demo.keystore 之前生成的证书

-signedjar demo_signed.apk 签名后的apk

demo.apk 需要签名的apk

demo.keystore 证书的别名

执行后会生成一个已签名成功的apk，你可以用这个包发布市场。

###### 3.3优化（可选）

使用Zipalign优化，Zipalign是一个android平台上整理APK文件的工具，它首次被引入是在Android 1.6版本的SDK软件开发工具包中。它能够对打包的Android应用程序进行优化， 以使Android操作系统与应用程序之间的交互作用更有效率，这能够让应用程序和整个系统运行得更快。

命令如下：
```
$ zipalign -v 4 HelloWorld-release-unsigned.apk HelloWorld.apk
```