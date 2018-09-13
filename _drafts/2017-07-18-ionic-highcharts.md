---
layout: post
title: ionic/angular 中使用 Highcharts
categories: ionic
description: ionic/angular 中使用 Highcharts
keywords: Html5, ionic, hybird, Highcharts
---

之前项目中有用到Highcharts，那个时候是用@ViewChild修饰器，但是最近看到Highcharts官方的案例，好像更简单一些，所以做一下记录。

> 之前项目中的用法可参考：https://github.com/xiedajian/ipvpKmfApp2.0/blob/master/src/pages/LoginModule/account-details/account-details.ts

### 介绍一下Highcharts 官方案例

###### 首先需要下载 Highcharts 包
```
npm install highcharts --save
```
接下来就是编写代码了，首先打开 src/pages/home/home.html 在合适的位置
###### 添加一个 div 容器
```
<div id="container"></div>
```
然后打开 home.ts （和上面的 home.html 在同一个目录），引入 highcharts 模块，并在 ionViewDidLoad 函数里编写图表代码，实例代码如下：

```
import { Component } from '@angular/core';
import { NavController } from 'ionic-angular';
import * as Highcharts from 'highcharts';

@Component({
    selector: 'page-home',
    templateUrl: 'home.html'
})
export class HomePage {
    constructor(public navCtrl: NavController) {
    }

    ionViewDidLoad(){
        var chart = Highcharts.chart('container', {
            title: {
                text: '不同城市的月平均气温',
                x: -20
            },
            subtitle: {
                text: '数据来源: WorldClimate.com',
                x: -20
            },
            xAxis: {
                categories: ['一月', '二月', '三月', '四月', '五月', '六月', '七月', '八月', '九月', '十月', '十一月', '十二月']
            },
            yAxis: {
                title: {
                    text: '温度 (°C)'
                },
                plotLines: [{
                    value: 0,
                    width: 1,
                    color: '#808080'
                }]
            },
            tooltip: {
                valueSuffix: '°C'
            },
            legend: {
                layout: 'vertical',
                align: 'right',
                verticalAlign: 'middle',
                borderWidth: 0
            },
            series: [{
                name: '东京',
                data: [7.0, 6.9, 9.5, 14.5, 18.2, 21.5, 25.2, 26.5, 23.3, 18.3, 13.9, 9.6]
            }, {
                name: '纽约',
                data: [-0.2, 0.8, 5.7, 11.3, 17.0, 22.0, 24.8, 24.1, 20.1, 14.1, 8.6, 2.5]
            }, {
                name: '柏林',
                data: [-0.9, 0.6, 3.5, 8.4, 13.5, 17.0, 18.6, 17.9, 14.3, 9.0, 3.9, 1.0]
            }, {
                name: '伦敦',
                data: [3.9, 4.2, 5.7, 8.5, 11.9, 15.2, 17.0, 16.6, 14.2, 10.3, 6.6, 4.8]
            }]
        });
    }
}

```

就是这么简单

![image.png](http://upload-images.jianshu.io/upload_images/4263048-998c2dd8726465f4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

同样的我们可以参考 [Highcharts 官方实例](https://www.hcharts.cn/demo/highcharts/dynamic-update) 编写一个实时刷新的例子，运行结果如下图


![image.png](http://upload-images.jianshu.io/upload_images/4263048-30fc4a898412b4c6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

[Highcharts：](https://www.highcharts.com)        

[案例来自官方：](http://blog.jianshukeji.com/create-chart-in-ionic-using-highcharts)