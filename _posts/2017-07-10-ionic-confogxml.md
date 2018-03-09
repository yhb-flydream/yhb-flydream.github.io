---
layout: post
title: ionic项目的config.xml的作用
categories: ionic
description: config.xml文件配置简单介绍
keywords: js, ionic, cordova, hybird, config.xml
---

[官方文档：](https://cordova.apache.org/docs/en/latest/config_ref/index.html)
[转自：](http://blog.csdn.net/zzh_receive/article/details/53191593?locationNum=1&fps=1)

# config.xml的作用
Config.xml用于控制一些app的行为，这个平台无关的xml文件是基于W3C的Packaged Web Apps(Widgets)描述标准，扩充特定的核心Cordova API功能，插件和特定平台设置

当通过Cordova命令行创建一个工程以后，在其根目录会有一个config.xml文件,当使用platform add命令添加指定的移动平台以后，会在platforms目录各自平台的子目录有一个config.xml的拷贝

```
app/platforms/ios/AppName/config.xml 
app/platforms/blackberry10/www/config.xml
app/platforms/android/res/xml/config.xml
```
# config.xml核心配置元素
```
<widgetid="com.example.hello"version="0.0.1"><name>HelloWorld</name><description> A sample Apache Cordova application that responds to the deviceready event. </description><authoremail="dev@callback.apache.org"href="http://cordova.io"> Apache Cordova Team </author><contentsrc="index.html" /><accessorigin="*" /></widget>
```

中的id用来标记app的标识符，同时我们也可以在这里设置versionCode，CFBundleVersion和packageVersion这类版本信息 
用于指定app的正式名称，在手机主页和app-store里面显示的名字。 
和用于配置程序的说明文字，作者。这些信息会出现在app-store的信息里面。 
用于设置app的启示页，该页默认为index.html，在工程根目录。 
此配置用来设置app可以访问哪些外部域下server的资源，具体参考Whitelist 
用于设置各个可选设置，每一个preference不区分大小写，有一些preference只针对特殊平台有效。下面是一些针对多平台有效的常见preference。
#共通参数
该参数用于设置app是否隐藏状态栏，在ios下是不隐藏状态栏的，但是会影响获取状态栏高度的准确值，默认为false。
```
<preferencename="Fullscreen"value="true" />
```

#支持多平台的参数设置
设置是否禁止滑动超出范围，此时会在超出部分显示黑色背景。在ios下如果设置为true，会引起拖拽页面的时候会触发放大显示功能。
```
<preferencename="DisallowOverscroll"value="true"/> #仅支持IOS&Android
```

主背景色。
```
<preferencename="BackgroundColor"value="0xff0000ff"/> #仅支持BlackBerry&Android
```

隐藏键盘显示时上面附带的status bar。
```
<preferencename="HideKeyboardFormAccessoryBar"value="true"/> #仅支持BlackBerry
```
锁定显示朝向landscape or portrait。
```
<preference name="Orientation" value="landscape" />
<platform name="android"> 
      <preference name="Orientation" value="sensorLandscape" /> 
</platform>
 <platform name="ios">
      <preference name="Orientation" value="all" />
 </platform>
```

为特定平台添加plugin。在使用cordova plugin add指令的时候会自动添加。
   ```
<feature name="Device"><param name="android-package" value="org.apache.cordova.device.Device" /></feature>
<feature name="Device"><param name="ios-package" value="CDVDevice" /></feature>
```

为指定平台单独设置属性。
```
<platform name="android"><preference name="Fullscreen" value="true" /></platform>
```

设置hook，具体参见Hook
```
<hook type="after_plugin_install" src="scripts/afterPluginInstall.js" />
```

# iOS的config.xml设置
EnableViewportScale (boolean, defaults to false) 如果设置成true，用于在viewport的meta标签是否生效。
 ```
<preferencename="EnableViewportScale"value="true"/>
```
MediaPlaybackAllowsAirPlay (boolean, defaults to true): 是否阻止使用airplay功能。
```
<preferencename="MediaPlaybackAllowsAirPlay"value="false"/>
```

MediaPlaybackRequiresUserAction (boolean, defaults to false) 是否阻止自动播放媒体文件。
```
<preferencename="MediaPlaybackRequiresUserAction"value="true"/>
```

AllowInlineMediaPlayback (boolean, defaults to false) 是否允许重放，需要在浏览器提供的标签内添加webkit-playsinline。
```
<preferencename="AllowInlineMediaPlayback"value="true"/>
```

BackupWebStorage (string, either none, local, or the default cloud) 选择程序备份的地点。
```
<preferencename="BackupWebStorage"value="local"/> #none不进行备份 #local 备份到本地iTurn #cloud 备份到via iCloud
```

TopActivityIndicator (string, defaults to gray) 用于设置顶部状态栏风格，可选参数whiteLarge, white, and gray。
```
<preferencename="TopActivityIndicator"value="white"/>
```

KeyboardDisplayRequiresUserAction (boolean, defaults to true) 是否禁止当输入框使用focus()获得焦点的时候显示键盘。
```
<preferencename="KeyboardDisplayRequiresUserAction"value="false"/> #绝大多数情况下我们应该设置成false，除非你不想让用户输入任何信息
```
SuppressesIncrementalRendering (boolean, defaults to false) 是否支持数据全部渲染完成后再显示到界面上。
```
<preferencename="SuppressesIncrementalRendering"value="true"/>
```

GapBetweenPages (float, defaults to 0) 界面间隙(ios UIWebView的配置参数)。
```
<preferencename="GapBetweenPages"value="0"/>
```

PageLength (float, defaults to 0) 每个界面的size(ios UIWebView的配置参数)。
```
<preferencename="PageLength"value="0"/>
```

PaginationBreakingMode (string, defaults to page) ios UIWebView相关的参数。
```
 可选值 page and column 
<preferencename="PaginationBreakingMode"value="page"/>
```

PaginationMode (string, defaults to unpaginated) 用于设置分页相关的，是ios UIWebView相关的设置。
```
 # 可选值 unpaginated, leftToRight, topToBottom, bottomToTop, and rightToLeft. 
<preferencename="PaginationMode"value="unpaginated"/>
```

UIWebViewDecelerationSpeed (string, defaults to normal) 用于设置滚动条滑动速度。
```
 # 可选值 normal, fast 
<preferencename="UIWebViewDecelerationSpeed"value="fast" />
```

ErrorUrl (string, not set by default) 设置错误信息页。
```
<preferencename="ErrorUrl"value="myErrorPage.html"/>
```
OverrideUserAgent (string, not set by default) 用于重新设置UserAgent信息。
```
<preferencename="OverrideUserAgent"value="Mozilla/5.0 My Browser" />
```
AppendUserAgent (string, not set by default) 在UserAgent末尾添加新内容。
```
<preferencename="AppendUserAgent"value="My Browser" /> #当OverrideUserAgent被设置时无效
```

target-device (string, defaults to universal) 设置支持设备类型，手机，平板，无限制。
```
 #可选值 handset, tablet, universal 
<preferencename="target-device"value="universal" />
```

deployment-target (string, not set by default) 设置支持的最低版本。
<preferencename="deployment-target"value="7.0" />
1

CordovaWebViewEngine (string, defaults to ‘CDVUIWebViewEngine’) 设置cordova引擎，一般没人会设置这个。
```
<preferencename="CordovaWebViewEngine"value="CDVUIWebViewEngine" />
```

SuppressesLongPressGesture (boolean, defaults to false) 是否绕过3Dtouch长按弹出一个放大窗口显示内容的功能。
```
<preferencename="SuppressesLongPressGesture"value="true" />
```

Suppresses3DTouchGesture (boolean, defaults to false) 是否绕过3Dtouch功能。
```
<preferencename="Suppresses3DTouchGesture"value="true" /> 
如果Suppresses3DTouchGesture为true，SuppressesLongPressGesture最好也要设置为true
```

CDVSystemSchemesOverride (string, defaults to maps,tel,telprompt) 设置允许被传送给系统的协。
```
<preferencename="CDVSystemSchemesOverride"value="maps,tel,telprompt" />
```

#Android的config.xml设置
KeepRunning (boolean, defaults to true): 决定是否允许app在pause后依然运行，设置成false在app接受pause的时候就不会被杀死了，只是暂停执行代码
```
<preferencename="KeepRunning"value="false"/>
```

LoadUrlTimeoutValue (number in milliseconds, default to 20000, 20 seconds): 用来设置加载一个页面的timeout时间。默认20秒。
```
<preferencename="LoadUrlTimeoutValue"value="10000"/>
```

SplashScreen (string, defaults to splash): 用于设定splash screen的启动图片的名字，这个名字在res/drawable目录。 在各自子目录里面设置同样名字的资源。
```
<preferencename="SplashScreen"value="mySplash"/>
```

SplashScreenDelay (number in milliseconds, defaults to 3000): splash screen的显示时长。
```
<preferencename="SplashScreenDelay"value="10000"/>
```

InAppBrowserStorageEnabled (boolean, defaults to true): 控制是否允许在InAppBrowser打开的web页面允许访问相同的localStorage和webSQL资源。
```
<preferencename="InAppBrowserStorageEnabled"value="true"/>
```
LoadingDialog (string, defaults to null): 用于设置在第一次加载页面的时候显示一个窗口，该窗口显示指定的title和message。
```
<preferencename="LoadingDialog"value="My Title,My Message"/>
```
LoadingPageDialog (string, defaults to null): 和LoadingDialog一样，但是在第一次加载每一个页面的时候都会显示。
```
<preferencename="LoadingPageDialog"value="My Title,My Message"/>
```

ErrorUrl (URL, defaults to null): 如果发生问题的话显示一个以Application Error为title的页面。
```
<preferencename="ErrorUrl"value="myErrorPage.html"/>
```

ShowTitle (boolean, defaults to false): 在屏幕顶端显示title。
```
<preferencename="ShowTitle"value="true"/>
```

LogLevel (string, defaults to ERROR): 设置log的等级，取值范围[ERROR, WARN, INFO, DEBUG, and VERBOSE]。
```
<preferencename="LogLevel"value="VERBOSE"/>
```

SetFullscreen (boolean, defaults to false): 此属性已经不赞成使用，会在将来删除 
AndroidLaunchMode (string, defaults to singleTop): 设置Activity的launchMode，和AndroidManifest.xml相同，具体参考android开发指南。可选值[standard, singleTop, singleTask, singleInstance]。
```
<preferencename="AndroidLaunchMode"value="singleTop"/>
```

DefaultVolumeStream (string, defaults to default, added in cordova-android 3.7.0): 设备的音量按钮相关设置，可以被设置成call或者media。
OverrideUserAgent (string, not set by default) 用于重新设置UserAgent信息。该设置会引起服务器issue，所以要谨慎使用。
```
<preferencename="OverrideUserAgent"value="Mozilla/5.0 My Browser" />
```

AppendUserAgent (string, not set by default) 在UserAgent末尾添加新内容。
```
<preferencename="AppendUserAgent"value="My Browser" /> #当OverrideUserAgent被设置时无效
```
####可以参考本人的guthub项目，欢迎star
传送门：https://github.com/xiedajian/ionic3_demo/blob/master/config.xml
