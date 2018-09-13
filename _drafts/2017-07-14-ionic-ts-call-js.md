---
layout: post
title: typescript 与 javascript 的互相调用
categories: ionic
description: typescript 与 javascript 的互相调用
keywords: js, ionic, cordova, hybird, typescript
---

### 源自网络：

ts 是 js 的超集，因此只要是 js 与 js 可以互相调用的，ts 均可以调用，只不过需要增加声明来解决编译时报错。

ts 最终生成的文件为 js，因此 js 调用 ts 其实就是 js 调用 js（ts 生成的 js 文件）。

### ts 调用 js

###### 步骤

找到 js 调用 js 的方法。

增加方法调用的声明。 请参考如何生成 .d.ts。

###### 示例

js 内的方法
```

functioncallJsFunc(msg){

console.log("msg from egret : "+msg);

}
```

#### ts 内声明

declare functioncall JsFunc(msg:string);//可以放在 ts 文件内（建议在顶部或者底部，中间的没试过）或者单独放到一个 .d.ts 文件中，请不要放在其他类型的文件内。msg 类型根据函数体判断。

#### ts 内调用

callJsFunc("hello js");

###### 输出

msg frome gret:hello js

#### 总结：在 js 调用 js 的基础上增加声明。其他的比如变量等，也是按上面步骤来实现。

### js 调用 ts

js 调用 ts 其实就是 ts 调用 ts，由于 ts 调用 ts 可能会有同模块下的省略写法，因此只要使用不同模块下的调用来写即可。

##### 步骤

找到非同一模块下 ts 的调用（比如example.A.CallEgretFunc("hello")）。

完全按上面调用的方式来写 (比如上面的example.A.CallEgretFunc("hello"))。

##### 示例

ts 内的方法
```

moduleexampleA{

exportclassA{

publiccallEgretMethod(msg:string):void{

console.log("method msg from js : "+msg);

}

publicstaticCallEgretFunc(msg:string):void{

console.log("static msg from js : "+msg);

}

}

}
```
非同一模块下 ts 调用
```

moduleexampleB{

exportfunctionb(){

//调用方法

vara:exampleA.A=newexampleA.A();

a.callEgretMethod("method");

//调用静态函数

exampleA.A.CallEgretFunc("function");

}

}
```
js 内调用
```
vara=newexampleA.A();//去掉 a 的类型

a.callEgretMethod("method");

exampleA.A.CallEgretFunc("function");
```

输出
```

method msgfromjs:method

staticmsgfromjs:function
```
#### 总结：相当于非同一个模块下的 ts 调用 ts。其他的比如变量等，也是按上面步骤来实现。
