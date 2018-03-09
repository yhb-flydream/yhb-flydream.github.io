---
layout: post
title: 关于ionic的Native插件的变化
categories: ionic
description: 关于ionic的Native插件的变化
keywords: js, ionic, cordova, hybird, native
---


### 从ionic1到ionic2的变化就不在记录，记录一下ionic2到ionic3之间的变化

#### 1.在ionic2刚开始的时候（可能到ionic2正式版刚出来的时候也是，记不清了），ionic的Native是集中在一起的，比如
```
import{CodePush}from'ionic-native';

import{ File }from'ionic-native';

import{Network}from"ionic-native";
```

可以看到，大多的插件都是从ionic-native@core中引入的，而且不需要在app.modile.ts中声明

#### 2.在ionic3中，每个插件都分开进行安装，减小核心包的大小。

例如安装camera插件
```

$ ionic cordova plugin add cordova-plugin-camera

$ npm install --save @ionic-native/camera
```

并且需要在app.modile.ts中集中声明

```
//native插件
import { AppMinimize } from '@ionic-native/app-minimize';
import {CodePush} from '@ionic-native/code-push';
import {CallNumber} from '@ionic-native/call-number';
import {AppVersion} from '@ionic-native/app-version';
import {Device} from '@ionic-native/device';
import {File} from '@ionic-native/file';
import {FileOpener} from '@ionic-native/file-opener';
import {Transfer} from '@ionic-native/transfer';
import {Network} from '@ionic-native/network';
import {StatusBar} from '@ionic-native/status-bar';
import {SplashScreen} from '@ionic-native/splash-screen';
```
然后添加在providers[]中
```
    providers: [
        AppMinimize,
        CodePush,
        AppVersion,
        CallNumber,
        Device,
        File,
        FileOpener,
        Transfer,
        Network,
        StatusBar,
        SplashScreen,
        // {provide: ErrorHandler, useClass: IonicErrorHandler},
        PopSer,
        HttpSer,
        CallSer,
        FileSer,
        NetworkSer,
        UpdateAppSer,
        AppInitSer,
        InterfaceLists,
        CustomerService,
        CRMService,
        DateService,
        CallNumberService
    ]
```


