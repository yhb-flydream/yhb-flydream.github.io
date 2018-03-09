---
layout: post
title: ionic管道pipe
categories: ionic
description: 自定义管道教程
keywords: js, ionic, cordova, hybird, pipes
---

[管道相关的资料：](https://www.angular.cn/docs/ts/latest/guide/pipes.html)
# 基础介绍：
管道可以在模板中转换显示的内容。管道把数据作为输入，然后转换它，给出期望的输出。
自定义组件如下：
```
import {Injectable, Pipe, PipeTransform} from '@angular/core';

@Pipe({
    name: 'numtotimePipe'
})
@Injectable()
export class NumToTimePipe implements PipeTransform {
    /*
     数字转分钟
     70  => 01:10"
     */
    transform(second:number):any {
        var mm:number = Math.floor(second / 60);
        var ss:number = Math.ceil(second % 60);
        let minute:string = mm < 10 ? ('0' + mm.toString()) : mm.toString();
        let seconds:string = ss < 10 ? ('0' + ss.toString()) : ss.toString();
        let r:string = minute + ":" + seconds + '"';
        return r;
    }

}
```
# ionic2.2.1中使用：
1.先在app.module.ts中声明
```
import {NumToTimePipe} from '../pipes/numtotimePipe';
```
2.加入app.module.ts文件declarations中
 ```
declarations: [
NumToTimePipe,]
``` 
3.在需要用到的页面
  ```
<span class="audio_duration">{{log.trackDetail.voiceRecordSize | numtotimePipe }}</span>
```
# ionic3.4.2中因为使用了懒加载，所以稍微有些变化
1.每个页面都编程了一个页面，都有自己的module.ts文件
2.写好众多的pipe管道封装成了一个模块，pipes.module.ts
```
import { NgModule } from '@angular/core';
import {CommonModule} from "@angular/common";
import { ContactTypePipe } from './contactTypePipe';
import { notContactReasonPipe } from './notContactReasonPipe';
import { NumToTimePipe } from './numtotimePipe';
import { TrackResultPipe } from './trackResultPipe';
import { DataSubstringPipe } from './dataSubstringPipe';

@NgModule({
    declarations: [
        ContactTypePipe,
        notContactReasonPipe,
        NumToTimePipe,
        TrackResultPipe,
        DataSubstringPipe,
    ],
    imports: [
        CommonModule
    ],
    exports: [
        ContactTypePipe,
        notContactReasonPipe,
        NumToTimePipe,
        TrackResultPipe,
        DataSubstringPipe,
    ]
})
export class PipesModule { }
```
3.在使用到管道的页面的module中
```
import { NgModule } from '@angular/core';
import { IonicPageModule } from 'ionic-angular';
import { TrackingLogPage } from './tracking-log';
import { PipesModule } from '../../../pipes/pipes.module';
// import { notContactReasonPipe } from '../../../pipes/notContactReasonPipe';
// import { NumToTimePipe } from '../../../pipes/numtotimePipe';
// import { TrackResultPipe } from '../../../pipes/trackResultPipe';
// import { DataSubstringPipe } from '../../../pipes/dataSubstringPipe';
@NgModule({
  declarations: [
    TrackingLogPage,
    // TrackResultPipe,
    // notContactReasonPipe,
    // NumToTimePipe,
    // DataSubstringPipe,
  ],
  imports: [
    PipesModule,
    IonicPageModule.forChild(TrackingLogPage),
  ],
  exports: [
    TrackingLogPage
  ]
})
export class TrackingLogPageModule {}
```
#### 可以参考本人的guthub项目，欢迎star
[GitHub](https://github.com/xiedajian/ipvpKmfApp2.0/tree/master/src/pipes)

