---
layout: post
title:  Ionic DevApp :非常好用的免费官方开发调试工具
categories: ionic
description:  Ionic DevApp是一个免费的应用程序，可以让您直接在iOS或Android设备上运行您的Ionic应用程序
keywords: ios , ionic , android ,DevApp ,js
---


Ionic DevApp是一个免费的应用程序，可以让您直接在iOS或Android设备上运行您的Ionic应用程序。

跳过处理令人沮丧的原生SDK安装问题，只需运行ionic serve，打开DevApp，连接到相同的网络，应用程序将自动加载并运行您的应用程序。

DevApp是一款100％免费的iOS和Android手机应用程序，可以让您直接在手机上测试应用程序。DevApp提供了一个实时的更改视图，并提供丰富的预装本机插件库来测试应用程序的每个功能。

DevApp自带了许多原生插件，因此您不必担心安装插件。

#### 使用

1）首先，确保你运行了最新版本的Ionic CLI npm install -g ionic
3）将您的设备和开发计算机连接到同一个WiFi网络。
2）手机安装Ionic DevApp。
4）在您的设备上打开DevApp。
5）ionic serve在您的电脑上运行，为您的应用程序提供服务 然后，您应该看到在DevApp上弹出的应用程序。
6）点击你的应用程序和繁荣，你现在有一个开发版本的应用程序运行在您的设备上，LiveReload和cordova插件的支持


注意：DevApp查找ionic serve在本地网络上运行的实例，并需要最新版本的Ionic CLI（至少版本3.13.2）。
##### 实例演示：1.打开手机端DevApp
![image.png](http://upload-images.jianshu.io/upload_images/4263048-9b118d9939afd9d3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##### 实例演示：2.手机端DevApp会自动搜索出在同一WIFI下的项目：
![image.png](http://upload-images.jianshu.io/upload_images/4263048-231743ea94f58564.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##### 实例演示：3.点击即可调试项目：
![image.png](http://upload-images.jianshu.io/upload_images/4263048-89b529b4f0694f05.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


#### 故障排除

如果您在列表中看不到您的应用程序，请尝试以下方法解决问题：

- 首先，确保你和应用程序在同一个网络上。仔细检查你的WiFi连接设置。
- 尝试强制退出DevApp并重新启动它
- 尝试ionic serve在您的计算机上重新启动。
如果这些东西仍然不能解决问题，请确保您没有任何自定义网络设置，可能导​​致应用程序无法发现服务实例。

#### DevApp内置插件列表
```
card.io.cordova.mobilesdk 2.1.0 "CardIO"
com-intel-security-cordova-plugin 2.0.3 "APP Security API"
com.darktalker.cordova.screenshot 0.1.5 "Screenshot"
com.paypal.cordova.mobilesdk 3.5.0 "PayPalMobile"
cordova-admob-sdk 0.8.0 "AdMob SDK"
cordova-base64-to-gallery 4.1.2 "base64ToGallery"
cordova-instagram-plugin 0.5.5 "Instagram"
cordova-launch-review 2.0.0 "Launch Review"
cordova-plugin-3dtouch 1.3.5 "3D Touch"
cordova-plugin-actionsheet 2.3.3 "ActionSheet"
cordova-plugin-add-swift-support 1.6.2 "AddSwiftSupport"
cordova-plugin-admob-free 0.10.0 "Cordova AdMob Plugin"
cordova-plugin-app-event 1.2.0 "Application Events"
cordova-plugin-apprate 1.3.0 "AppRate"
cordova-plugin-battery-status 1.2.4 "Battery"
cordova-plugin-ble-central 1.1.4 "BLE"
cordova-plugin-bluetooth-serial 0.4.7 "Bluetooth Serial"
cordova-plugin-brightness 0.1.5 "Brightness"
cordova-plugin-calendar 4.6.0 "Calendar"
cordova-plugin-camera 2.4.1 "Camera"
cordova-plugin-compat 1.1.0 "Compat"
cordova-plugin-console 1.0.7 "Console"
cordova-plugin-contacts 2.3.1 "Contacts"
cordova-plugin-datepicker 0.9.3 "DatePicker"
cordova-plugin-device 1.1.6 "Device"
cordova-plugin-device-motion 1.2.5 "Device Motion"
cordova-plugin-device-orientation 1.0.7 "Device Orientation"
cordova-plugin-dialogs 1.3.3 "Notification"
cordova-plugin-email-composer 0.8.7 "EmailComposer"
cordova-plugin-geolocation 2.4.3 "Geolocation"
cordova-plugin-globalization 1.0.7 "Globalization"
cordova-plugin-google-analytics 1.8.3 "Google Universal Analytics Plugin"
cordova-plugin-health 1.0.0 "Cordova Health"
cordova-plugin-image-picker 1.1.1 "ImagePicker"
cordova-plugin-inappbrowser 1.6.1 "InAppBrowser"
cordova-plugin-insomnia 4.3.0 "Insomnia (prevent screen sleep)"
cordova-plugin-intercom 3.2.2 "Intercom"
cordova-plugin-ionic 1.1.6 "IonicCordova"
cordova-plugin-ios-keychain 3.0.1 "KeyChain Plugin for Cordova iOS"
cordova-plugin-media 3.0.1 "Media"
cordova-plugin-mixpanel 3.1.0 "Mixpanel"
cordova-plugin-music-controls 2.0.0 "MusicControls"
cordova-plugin-nativeaudio 3.0.9 "Cordova Native Audio"
cordova-plugin-nativestorage 2.2.2 "NativeStorage"
cordova-plugin-network-information 1.3.3 "Network Information"
cordova-plugin-request-location-accuracy 2.2.1 "Request Location Accuracy"
cordova-plugin-safariviewcontroller 1.4.7 "SafariViewController"
cordova-plugin-screen-orientation 2.0.1 "Screen Orientation"
cordova-plugin-secure-storage 2.6.8 "SecureStorage"
cordova-plugin-shake 0.6.0 "Shake Gesture Detection"
cordova-plugin-sim 1.3.3 "SIM"
cordova-plugin-splashscreen 4.0.3 "Splashscreen"
cordova-plugin-statusbar 2.2.3 "StatusBar"
cordova-plugin-stripe 1.5.3 "cordova-plugin-stripe"
cordova-plugin-taptic-engine 2.1.0 "Taptic Engine"
cordova-plugin-themeablebrowser 0.2.17 "ThemeableBrowser"
cordova-plugin-touch-id 3.2.0 "Touch ID"
cordova-plugin-tts 0.2.3 "TTS"
cordova-plugin-vibration 2.1.5 "Vibration"
cordova-plugin-whitelist 1.3.2 "Whitelist"
cordova-plugin-x-socialsharing 5.1.8 "SocialSharing"
cordova-plugin-x-toast 2.6.0 "Toast"
cordova-plugin-zip 3.1.0 "cordova-plugin-zip"
cordova-promise-polyfill 0.0.2 "cordova-promise-polyfill"
cordova-sms-plugin 0.1.11 "Cordova SMS Plugin"
cordova-sqlite-storage 2.0.4 "Cordova sqlite storage plugin"
cordova-universal-clipboard 0.1.0 "Clipboard"
de.appplant.cordova.plugin.local-notification 0.8.5 "LocalNotification"
de.appplant.cordova.plugin.printer 0.7.1 "Printer"
ionic-plugin-keyboard 2.2.1 "Keyboard"
phonegap-nfc 0.6.6 "NFC"
phonegap-plugin-barcodescanner 6.0.7 "BarcodeScanner"
phonegap-plugin-mobile-accessibility 1.0.5-dev "Mobile Accessibility"
uk.co.workingedge.phonegap.plugin.launchnavigator 4.0.4 "Launch Navigator"
```