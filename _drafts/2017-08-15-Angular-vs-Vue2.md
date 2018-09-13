---
layout: post
title: 聊聊技术选型- Angular2 vs Vue2[转]
categories: js
description: Angular2 vs Vue2对比
keywords: js, Angular2, Vue2
---


##### 作者介绍：李旸，美团点评前端工程师，3 年 Web 前端开发经验，现在是美团点评点餐团队的一员。


*"Come, and take choice of all my library, And so beguile thy sorrow." —— William Shakespeare, Titus Andronicus*
为项目进行框架级别的技术选型，就类似为篮球队量身定制战术，选择一个适合开发团队的规模和团队成员的技术栈和能力，针对业务和项目，能帮助团队赢得更多的技术，是每个软件项目能够顺利推进的先决条件，也是业务常青的有效的保障。这里，我们来聊聊为一个新的前端项目挑选一个合适的技术模型，对比在去年都发布了 release 版本的 Angular2 和 Vue2（以下如没有特别指明，Angular 即为 Angular2，Vue 即为 Vue2），并不作鱼和熊掌哪个更美味的选择，而是站在技术本身，对应项目和开发人员的角度，帮助工程师在所处的业务场景下挑选最好的武器。

![image.png](http://upload-images.jianshu.io/upload_images/4263048-f3f78a579ce77368.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

目前没法确切的评估未来一段时间这两个框架的维护情况，但基本能确定的是，框架的生命周期不会比我们大部分业务的生命周期短。Angular 的缺点在于，除了核心之外，像 core-[js](http://lib.csdn.net/base/javascript)，rxjs，zone.js 等生产环境依赖的系统不是 Google 的人主导的，存在潜在质量问题的可能性，并且 Angular 目前已经发布了 Angular4 的 rc 版本（主版本跳过了 Angular3 ），后面预计半年进行一次主版本的更新，虽然相关开发人员承诺尽可能向下兼容，但是后续对主版本的频繁升级对项目的影响还是个未知数；Vue 由于作者是中国人，在国内推广的很好，口碑很不错，作者也清理 GitHub issue 的速度也非常快，坑会相对更少一些，后面也和阿里合作成为了 Weex 的官方框架，而 Angular 在国内目前形势还不是很清晰，主要原因可能在于中文资料的数量远远小于英文资料。从国内的使用情况以及社区发展来看，Vue 更胜一筹。


![image.png](http://upload-images.jianshu.io/upload_images/4263048-c54a1da4dd974f31.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


为了避免前端组件缺乏一致的管理方式，重造轮子，解决多人在快速迭代中协作开发导致的代码逐渐混乱，[javascript](http://lib.csdn.net/base/javascript) 的动态类型增加了重构难度的情况，我们希望引入静态语言，通过类型检查使数据更清晰，通过接口规范开发行为，这一点 Angular 通过默认引入 Typescript 比 Vue 做的更好。Typescript 虽然本身是微软公司的产品，但是从编译器效率到使用体验均比目前的 Javascript 要强，在编写 ES6+ 代码时，经常因为 Babel 插件质量问题导致的坑，能避免很多。

![image.png](http://upload-images.jianshu.io/upload_images/4263048-68dc3ce5ee6c054c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

项目搭建工具
[ng-cli](https://github.com/angular/angular-cli)
[vue-cli](https://github.com/vuejs/vue-cli)

debug工具
[Augruy](https://chrome.google.com/webstore/detail/augury/elgalmkoelokbchhkhacckoklkejnhcd)
[vue-devtools](https://chrome.google.com/webstore/detail/vuejs-devtools/nhdogjmejiglipccpnnnanhbledajbpd)

[ng-cli](https://www.youtube.com/watch?v=uBRK6cTr4Vk&t=436s) 提供了包括从开发阶段架设前端 server 服务，代码生成，查阅文档，[测试](http://lib.csdn.net/base/softwaretest)，到部署过程的构建等的一系列指令，相比 vue-cli 只提供基础的项目初始化和构建功能，ng-cli 更好用。在 debug 工具层面，Vue 做的更好，vue-devtools 整合了 Vue 的状态管理工具 vuex，而使用 Angular 的状态管理方案 [ngrx](https://github.com/ngrx) 的时候，则需要配合 [Redux DevTools Extension](https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd)。
除了 ng-cli，[angular2-webpack-starter](https://github.com/AngularClass/angular2-webpack-starter) 也提供了完整的 Angular + Webpack 的种子项目。我们也可以根据业务调整具体的构建过程。
设计

从设计上看，Angular 提供了难以撼动的全面的解决方案，基本照顾到了开发流程的每个节点，他的 Form 支持，DI，测试流程，都是在开发体验上优于 Vue 的点，但是为了追求全面性，Angular 就无法避免的存在构建后体积大小和整个框架侵入性太强的问题。而 Vue 作为渐进增强的框架，不在一开始就在使用场景和模式上限制用户，而是通过官方提供的扩展，以及第三方扩展，逐渐为更复杂的需求场景提供解决方案，也给用户提供了选择的余地。
 

![image.png](http://upload-images.jianshu.io/upload_images/4263048-f4b2c0303483b61f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


性能
我们截取[ Vue 官方文档](https://cn.vuejs.org/v2/guide/comparison.html)上关于两个框架性能的对比报告截图。对比了 Angular 在去年 8 月发布的 rc 版本和同期 Vue beta 版本的不同操作的性能。可以看出，两个框架都非常的快，Angural 和 Vue 在大多操作上性能指标均处同一个数量级，Vue 在部分指标上略胜一筹。
![](http://upload-images.jianshu.io/upload_images/4263048-0ecd4a29ba5c11a3.jpeg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
在内存占用上，Vue 要优于 Angular，但是 Angular 框架本身提供了非常多的特性，而 Vue 在开发过程中引入 vue-router，vuex，vue-class-component 逐步发展为 Vue 全家桶的过程中，会逐步增长对内存的需求。
![](http://upload-images.jianshu.io/upload_images/4263048-6d1c41d24f729e20.jpeg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

开发模式
从学习曲线上看，Angular 要更陡峭，Vue 要相对平缓一些。在Web Componnet，PWA 上，Angular 要比 Vue 走的更远，更适合未来的标准，面向 Google 自己的技术栈。从能够开发的应用的全面性上，Angular 和 Vue 相差无几。
 

![image.png](http://upload-images.jianshu.io/upload_images/4263048-6c55e79c12b9b379.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

Native App
Nativescript + Angular
[Weex](https://weex.incubator.apache.org/cn/)

Desktop App
[angular-electron](https://github.com/angular/angular-electron)
[electron-vue](https://github.com/SimulatedGREG/electron-vue)

弹性
在业务开发中，技术选型并不能仅仅满足当前的业务需求的需要，而要考虑当前业务的状态，是刚刚开始，持续发展，还是稳定维护。考虑到业务后期可能出现的增长情况，这就要求我们选择的技术具备一定的弹性，能够随着业务伸缩，避免后期维护成本过高，扩展困难的情况的发生。

这里截取了[前端框架选型迁移的统计情况](https://github.com/YoungLeeNENU/eigenstuff)。y 轴代表迁移之前的选型，x 轴代表迁移之后的选型。表格中颜色越深，代表从选型 A 到选型 B 进行迁移的案例越多。可以发现，大家最多选型迁移的目标是 React，选择迁移到 Angular 的案例要比选择迁移到 Vue 的案例多，选择迁移到 Vue 的，绝大多数是 React 用户（相反从 Vue 迁移到 React 的用户也有一定数量）；而从 Angular 或 Vue 迁移到其他框架的案例较少，侧面证明了这两个框架在目前业界具备足够的弹性

![](http://upload-images.jianshu.io/upload_images/4263048-d551476ba380e55a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

业务场景
这里我们以点评点餐的内部数据系统为例。我们把系统对不同前端使用场景的频率和要求从0到10进行打分，分值越高的，相应场景的需求要求就越高，反之就越低。我们发现，我们的需求集中在图表绘制，组件管理和表单的提交校验上。数量较多的组件对于我们的组件管理方式提出了较高的要求；在已有的系统中我们对 highcharts 和 echarts 都有依赖，但是将逐步把图表组件迁移到 echarts 上。对于echarts，目前有[vue-echarts](https://github.com/Justineo/vue-echarts)，对于highcharts，有人做了[angular2-highcharts](https://github.com/gevgeny/angular2-highcharts)。
 

![image.png](http://upload-images.jianshu.io/upload_images/4263048-af76bd056c8a5f01.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


开发人员
目前点餐数据系统日常人力 1 人，对多人协作开发要求比较低，开发效率要求比较高，单个项目规模不大，有多端多项目开发的要求，技术选型能够适应快速迭代是一个目标，最大程度上的减少人力瓶颈的出现。
结论
首先，技术上对比 Angular 和 Vue，都是值得长线投资的技术。Angular 提供大一统式的解决方案，从浏览器端，服务端，客户端都有涉及，这种大一统的方案，优点在于在几乎任何场景，框架都提供了标准化的行为，而 Angular 通过一种侵入式较强的编程范式，规范了使用框架的所有开发者的开发行为，更工程化，更适合大型项目多人协作，同时，框架本身更拥抱标准，面向新特性，后面发展空间很大，而缺点是，这种大一统的方案，无法单独由谷歌提供，谷歌除了开发 Angular 的核心模块之外，在异步处理，状态管理，周边工具，使用了为数不少的第三方的库或组件，这些库和组件的行为是否会出现问题，和后续发展，很难预测，潜在增加了风险，这些第三方的库和组件，也有降低应用性能的可能性。
Vue 的切入角度是，这个框架可以被不同程度的使用，可以单独使用核心组件的部分，也可以加入状态管理，也可以加入路由管理，从一部分使用 Vue 到全站使用 Vue 开发，提供了开发者更多的选项，也借鉴了不同的框架，并对其优点单独为 Vue 进行了增强。这种精简和灵巧，非常适合项目初期的快速迭代，性能上，也没有很大缺陷，随着项目发展，性能也不会成为明显的问题。Vue 的潜在问题在于，由于提供了开发选项，在多人协作开发的情况下，不同开发者对于 Vue 使用程度和场景的处理可能会不一样，而随着项目增长，以“快”为特点的技术，在工程化和代码的管理上可能会出现困难，而像 Angular 提供的 DI 等功能，Vue 实现类似的功能就需要程序员进行手动控制，带来了潜在的代码管理的问题，目前虽然业界有不少使用 Vue 的场景，但是大型线上在稳定发展期业务，几乎是没有的。使用 Vue 在项目规模变大后，怎么处理 Vue 在项目中的地位，怎么组织代码，都是我们需要考虑的。
在我们的业务和人力层面，我们对数据平台[架构](http://lib.csdn.net/base/architecture)的规划是多端多层的，架构层服务于应用层，应用层服务于用户。对于用户层，新开始的项目面临逻辑经常调整的可能性，也就是说对于应用层，我们需要一个灵活，能够适应快速迭代的框架，而应用层的多种设备多种环境，也要求我们对性能要有起码的考虑，目前现有的组件和库，也希望新的框架能够做较好的兼容和提供现成的解决方案。这种情况下，Vue 是比较推荐的，后期随着应用端发展，Vue 能够确保没有性能瓶颈，也给了我们后期引入更多 Vue 解决方案，形成 Vue 全家桶或者撤掉 Vue，用其他方案的空间。而对于架构层，它发展的速度未必有应用层快，它对业务的要求是稳定，能够增量开发，尽量避免推倒重来影响应用层，同时，它性能的要求明显没有应用层高，这种情况，我们需要单独区分一下，例如如果需要做应用层的通用配置系统，配置应用层的 UI 组件，那么显然这个系统的组件框架要和应用层一致，而像自助查询平台或其他项目，我们可以使用 Angular，为后来的技术栈做技术储备。
对于新项目，我们技术选型可能未必选择一种，可以根据特点和业务都进行尝试，使用一段时间后，反馈给整个团队，这样，对不同的框架，我们后期都有技术储备，能保证我们手里能打的牌较多，不至于因为需求变的被动。所以我们在点餐数据产品中，Angular 和 Vue 都进行了尝试，也将在后续文章中，分享两个不同技术栈在日常开发细节上我们的积累。
转载：https://juejin.im/post/58cab85b44d9040069f38f7a