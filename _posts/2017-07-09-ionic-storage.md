---
layout: post
title: ionic的本地数据存储
categories: ionic
description: ionic的本地数据存储
keywords: js, ionic, cordova, hybird, hooks
---
#### ionic3开始storage默认使用的是IndexedDB，而不是LocalStorage

[官方文档：](http://ionicframework.com/docs/storage/)

### 存储

存储是存储键/值对和JSON对象的简单方法。存储使用下面的各种存储引擎，根据平台选择最佳的存储引擎。

当在本机应用程序环境中运行时，Storage将优先使用SQLite，因为它是最稳定和广泛使用的基于文件的数据库之一，并避免了诸如本地存储和IndexedDB之类的一些陷阱，例如操作系统决定清除这种数据在磁盘空间不足的情况下。

当在网络中运行或作为逐行Web应用程序运行时，Storage将按顺序尝试使用IndexedDB，WebSQL和localstorage。

### 用法

首先，如果要使用SQLite，请安装cordova-sqlite-storage插件：
```

ionic cordova plugin add cordova-sqlite-storage
```

接下来，安装软件包（默认情况下为Ionic应用程序> Ionic V1）：

```
npm install --save @ionic/storage
```

接下来，将它添加到您的NgModule声明中的导入列表中（例如，insrc/app/app.module.ts）：

```
import { IonicStorageModule } from '@ionic/storage';

@NgModule({
  declarations: [
    // ...
  ],
  imports: [      
    BrowserModule,
    IonicModule.forRoot(MyApp),
    IonicStorageModule.forRoot()
  ],
  bootstrap: [IonicApp],
  entryComponents: [
    // ...
  ],
  providers: [
    // ...
  ]
})
export class AppModule {}
```

最后，将其注入您的任何组件或页面：
```
import { Storage } from '@ionic/storage';

export class MyApp {
  constructor(private storage: Storage) { }

  ...

  // set a key/value
  storage.set('name', 'Max');

  // Or to get a key/value pair
  storage.get('age').then((val) => {
    console.log('Your age is', val);
  });
}
```
配置存储

存储引擎可以配置为特定的存储引擎优先级，也可以自定义配置选项传递给localForage。有关可能的选项，请参阅localForage配置文档：https：//github.com/localForage/localForage#configuration

注意：任何自定义配置将与默认配置合并

```
import { IonicStorageModule } from '@ionic/storage';

@NgModule({
  declarations: [...],
  imports: [
    IonicStorageModule.forRoot({
      name: '__mydb',
         driverOrder: ['indexeddb', 'sqlite', 'websql']
    })
  ],
  bootstrap: [...],
  entryComponents: [...],
   providers: [...]
})
export class AppModule { }
```