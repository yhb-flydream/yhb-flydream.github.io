---
layout: post
title: artTemplate前端模板引擎笔记
categories: js
description: artTemplate入门demo。
keywords: js, artTemplate, 命名规范
---

### 前言


最近jquery用的比较多，在遍历操作dom的时候，深感拼接字符串的痛苦，所有找了一个前端的模板引擎来动态编译模板。


#### artTemplate
地址：https://aui.github.io/art-template/
github：https://github.com/aui/art-template
##### 关于性能：
![image.png](http://upload-images.jianshu.io/upload_images/4263048-9939db23d23e490d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
#### 模板
art-template 同时支持两种模板语法。标准语法可以让模板更容易读写；原始语法具有强大的逻辑处理能力。
**标准语法**
```
{{if user}}
<h2>{{user.name}}</h2>
{{/if}}
```
**原始语法**
```
<% if (user) { %>
<h2><%= user.name %></h2>
<% } %>
```

原始语法兼容 [EJS](http://ejs.co/)、[Underscore](http://underscorejs.org/#template)、[LoDash](https://lodash.com/docs/#template) 模板。
#### 渲染模板
```
var template = require('art-template');
var html = template(__dirname + '/tpl-user.art', {
user: {
name: 'aui'
}
});
```

##### [](https://aui.github.io/art-template/docs/#核心方法)核心方法
```
// 基于模板名渲染模板
template(filename, data);

// 将模板源代码编译成函数
template.compile(source, options);

// 将模板源代码编译成函数并立刻执行
template.render(source, data, options);
```

上面是官方的介绍，下面一个自己做的简单例子：
##### demo
```
<!DOCTYPE html>
<html lang="en">

    <head>
        <meta charset="UTF-8">
        <title>Title</title>
        
        <!--百度压缩版cdn引用地址:-->
        <script src="http://libs.baidu.com/jquery/1.7.2/jquery.min.js"></script>
        <!--引入模板引擎arttemplate-->
        <script src="../lib/template-web.js"></script>
    </head>

    <body>
        <!--容器1-->
        <div id='container1'>
            <!--模版1-->
            <script type="text/html" id='template1'>
                <ul id="list">
                    {{each list as li index}}
                        <li>{{index}}:{{li.name}}的年龄{{li.age}}</li>
                    {{/each}}
                </ul>
            </script>

        </div>

        <!--容器2-->
        <div id='container2'>
        </div>

        <!--容器3-->
        <div id='container3'>

        </div>

        <script>
            //artTemplate官网: https://aui.github.io/art-template/

            //总的开说，有三种用法
            //第一种，页面中已经用script标签定义好模版，取好id，根据模板名渲染模板。
            //API:template(filename, content);  根据模板名渲染模板。
            //注意:只能使用页面定义好的模板，不可以引用外部的文件为模板
            //1.1先把定义好的模板id加上数据，编译成html
            var html = template('template1', {
                list: [
                    {name:'wang',age:20},
                    {name:'zhu',age:21},
                    {name:'sun',age:22},
                ]
            });
            //1.2把编译好的html放到目标位置
            document.getElementById('container1').innerHTML = html;

            //第二种方法，先编译模版，再向模板添加数据，生成html
            //API:template.compile(source, options);  编译模板并返回一个渲染函数。
            //注意:可以引用外部的文件作为模板。例如用ajax.get来获取模板
            //2.1 把字符串编译成模板
            var templateStr = '<p>{{data}}</p>';
            var render = template.compile(templateStr);
            //2.2 向模板添加数据，组装模板
            var html = render({
                data: '这是传过去的数据'
            });
            //2、3 将编译好的html放到目标位置
            document.getElementById('container2').innerHTML = html;

            //第三种方法，编译模版生成html
            //API:template.render(source, data, options);  编译并返回渲染结果。
            var html = template.render('hi, <%=value%>.', {
                value: 'aui'
            });
            document.getElementById('container3').innerHTML = html;

            /*==================案例====================*/
            //案例：引入外部模板文件渲染

            //动态引入外部css
            function loadCss(url) {
                var link = document.createElement("link");
                link.type = "text/css";
                link.rel = "stylesheet";
                link.href = url;
                document.getElementsByTagName("head")[0].appendChild(link);
            };

            //引入外部模板和css
            function useTemplate(htmlUrl, cssUrl = '') {
                if(htmlUrl == '') return;
                if(cssUrl) {
                    loadCss(cssUrl);
                }
                $.get(htmlUrl, function(data) {
                    console.log(data);
                    var render = template.compile(data);
                    var html = render({content:'这是传过去的提示内容'});
                    console.log(html);
                    document.getElementById('container3').innerHTML = html;
                });
            }
            
            useTemplate('alert_template.html', 'alert_template.css');
            
            setTimeout(function() {
                $('.please-login-mask').css('display', 'block');
            }, 1000);
        </script>
    </body>
</html>
```
##### 外部模板文件 alert_template.html
 ```

<!--模拟的弹窗-->
<div class="please-login-mask">
    <div class="login-div">
        <p class="header">提示</p>
        <p class="content">{{content}}</p>
        <a href="javascript:;" class="queren">确认</a>
        </p>
    </div>
```
##### 外部模板文件对应的css alert_template.css
```
    /*模拟弹窗*/
    
    * {
        padding: 0;
        margin: 0;
    }
    a:link{
        text-decoration: none;
    }
    
    .please-login-mask {
        position: absolute;
        top: 0;
        bottom: 0;
        left: 0;
        right: 0;
        display: none;
        width: 100%;
        background-color: rgba(0, 0, 0, 0.5);
        z-index: 11;
    }
    
    .please-login-mask .login-div {
        height: 120px;
        width: 240px;
        position: absolute;
        top: 50%;
        left: 50%;
        margin-top: -60px;
        margin-left: -120px;
        background-color: white;
        border-radius: 10px;
        text-align: center;
    }
    
    .please-login-mask .header {
        height: 45px;
        font-size: 20px;
        line-height: 45px;
        color: #000000;
    }
    
    .please-login-mask .content {
        height: 30px;
        font-size: 14px;
        line-height: 30px;
        color: #000000;
    }
    
    .please-login-mask .queren {
        display: block;
        height: 45px;
        width: 100%;
        line-height: 45px;
        font-weight: 700;
        color: dodgerblue;
        border-top: 1px solid #C0C0C0;
    }
```
[demo的github地址：](https://github.com/xiedajian/artTemplateDemo/blob/master/template.html)