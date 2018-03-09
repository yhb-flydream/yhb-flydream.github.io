---
layout: post
title: ionic2/3全局变量
categories: ionic
description: ionic3没有全局变量，怎么自定义全局变量
keywords: js, ionic, cordova, hybird
---

在实际项目中，难免会有一些配置项需要来全局来配置，比如用户的信息，测试环境与生产环境的请求地址切换等，在ionic1中有全局变量rootscape，在ionic2/3中没有全局变量，所以我们就用一个公共类来存储这些全局变量

例如：

在app目录下新建app.config.ts文件,并新建类AppConfig,在类里面创建静态方法


```
/**
 * App配置信息
 */
export class AppConfig {
    static PCmodel:boolean = false;        //PC端调试模式
    static Appmodel:number=3;             //1首次启动  2.今日首次启动 3普通模式启动
    //设备信息
    static deviceId:string = '';          //设备id
    static deviceCordova:string = '';          //设备上运行的Cordova版本
    static deviceModel:string = '';           //设备型号或产品的名称
    static devicePlatform:string = '';          //操作系统名称
    static devicePlatformVersion:string = '';          //操作系统版本
    static deviceManufacturer:string = '';          //设备的制造商
    static deviceSerial:string = '';          //设备硬件序列号
    //APP信息
    static platform:string = '';          // android  ios
    static appName:string = 'CRM_KmfApp';           //CRM_KmfApp
    static appVersion:string = '2.0.2';        //版本号 2.0.2
    //常规配置
    static userProtocol:string = '';      //用户协议
    //导购用户信息
    static userName:string = '';          //账号名
    static token:string = '';             //token
    static userInfo:any = {};             //用户信息
    //导购配置信息
    static callingType:number = 2;        //通话方式      [1,2,3] 1免费 2普通  3两者
    static inited:boolean=true;              //系统是否可用 (指该执行人员归属的数据是否准备完毕)
    static balanceMinute:number = 0;      //剩余通话分钟数
    static showCustomerPhone:boolean=false;   //是否显示会员电话号码（导购可见）
    //授权信息
    static expireDate:any = '2018.01.01';           //APP到期日期
    //极光推送
    static jPushRegistrationId:string='';            //极光的注册id;
    static jPushAlias:string='';                //极光的别名;
    static jPushTags:string='';                //极光的标签;


    //获取设备高度
    public static getWindowHeight() {
        return window.screen.height;
    }

    //获取设备宽度
    public static getWindowWidth() {
        return window.screen.width;
    }
}

```


然后再需要使用全局变量的地方导入AppConfig

import{ AppConfig }from'./../../app/app.config';

最后通过AppConfig.platform即可获取平台名称。