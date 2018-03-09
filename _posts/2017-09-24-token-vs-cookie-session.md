---
layout: post
title: token代替cookie-session来维护用户身份状态
categories: js
description: token代替cookie-session来维护用户身份状态
keywords: js, token, session
---


在做用户身份认证及身份信息存储的时候，通常有cookie-session或者使用token两种方式。

####  token与session：

在存储过等同的情况下，在只是简单运用上，我只能说session与token没有本质的区别，二者不都是一串被加密过的字符串，拿他来做校验都一样。

以上，是因为你把token拿来当作用户是不是当事人做这么一个简单的校验的情况下。

当然，如果我们抛开一些比较极端的操作，token比session也有很大的区别：

- token可以存在任何位置（cookie、local storage）
- token比session更容易跨域。
- CORS预检查时token比较更简单。
- token有更多的控制权，比如当token过期时，你可以拿通过刷新token，让用户一直保持有效登录。
等……


其实如果你只是单纯拿着token做一下自己网站内用户登录检验的话是无太多区别的。

但假如token指的是OAuth Token提供认证和授权这类机制的话，那么就可以把session甩开N条街了，甚至是已经完全是两种不同的概念。

假设有这么一个场景，你们用户在你们网站产生的订单，而另一家公司是专业ERP公司；而你的用户希望他的订单同时授权给这家ERP公司使用的情况下，难道你希望用户拿在你家网站的用户名和密码给这家ERP公司吗？

这时候OAuth Token就有意义了，OAuth Token的授权大概是这样的：

- ERP需要调用我们提供的登录界面。
- 用户输入用户名和密码后，我们再向ERP发送一个TOKEN。
- ERP拿TOKEN换数据。
总之，如果你只是在自己网站内部上使用二者没有什么太多区别。而如果你的API是在不同终端上使用，token会更方便。

####  手机app使用token更合适


Cookie验证对于iOS来说很是繁琐的，比如说有些接口不需要验证，或者说就不能加上验证的，用Cookie的话也会自动发过去，需要手动清除Cookie，之后再添加；但是用Token就比较好控制发还是不发，毕竟是GET或者POST参数嘛 
再一个麻烦的就是Cookie在App关闭在开启之后会被重置，这个时候就需要做很多缓存的工作了，比较头疼，不如Token直接存在Keychain里面，每次要用的时候读取来的方便

token机制是为了防止cookie被清除，另外cookie是会在所有域名请求都携带上，无意中增加了服务端的请求量，token只需要在有必要的时候携带。token的中文名字就是令牌。。。。不是个多么高大上的东西

App通常用restful api跟server打交道。Rest是stateless的，也就是app不需要像browser那样用cookie来保存session, 因此用session token来标示自己就够了，session/state由api server的逻辑处理



#### 安全性token更好
可以对比一下三种认证方式的区别，这也是很基础的事情了 
1. basic auth 
没有安全性可言，完全依赖 https，并且每次请求都需要传递密码，是最不安全的 

2. session 
一般需要 basic auth 或其它 auth 方式先进行身份认证后才能建立，和 basic auth 一样没有什么安全性可言，需要 https 保障，只不过避免了每次传递密码（忽略服务器端状态这点特性） 

3. oauth 
部分是为了解决 basic auth 的安全问题而设计的，但是要复杂很多，即使没有https也能保证基本的安全，数据包被监听后不能防止信息泄露，但可以防止信息伪造，包括重放攻击


#### 扩展方便token更好 
Session 是一种HTTP存储机制，目的是为无状态的HTTP提供的持久机制。所谓 Session 认证只是简单的把 User 信息存储到 Session 里，因为 SID 的不可预测性，暂且认为是安全的。这是一种认证手段。 

而 Token ，如果指的是 OAuth Token 或类似的机制的话，提供的是 认证 和 授权 ，认证是针对用户，授权是针对 App 。其目的是让 某App 有权利访问 某用户 的信息。这里的 Token 是唯一的。不可以转移到其它 App 上，也不可以转到其它 用户 上。 

转过来说 Session 。Session 只提供一种简单的认证，即有此 SID ，即认为有此 User 的全部权利。是需要严格保密的，这个数据应该只保存在站方，不应该共享给其它网站或者第三方App。 

所以简单来说，如果你的用户数据可能需要和第三方共享，或者允许第三方调用 API 接口，用 Token 。 
如果永远只是自己的网站，自己的 App ，用什么就无所谓了。

在做SSO单点登录与 OAuth2.0授权时候，明显token更合适一些
