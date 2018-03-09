---
layout: post
title: Sass ,Scss 简单教程
categories: css
description: Sass ,Scss 简单教程
keywords: css, Sass, Scss
---

### Sass (Syntactically Awesome StyleSheets)
Sass 是对 CSS 的扩展，让 CSS 语言更强大、优雅。 它允许你使用[变量](http://sass.bootcss.com/docs/sass-reference/#variables_)、[嵌套规则](http://sass.bootcss.com/docs/sass-reference/#nested_rules)、 [mixins](http://sass.bootcss.com/docs/sass-reference/#mixins)、[导入](http://sass.bootcss.com/docs/sass-reference/#import)等众多功能， 并且完全兼容 CSS 语法。 Sass 有助于保持大型样式表结构良好， 同时也让你能够快速开始小型项目， 特别是在搭配 [Compass 样式库](http://compass-style.org/)一同使用时。
### 特色
- 完全兼容 CSS3
- 在 CSS 语言基础上添加了扩展功能，比如变量、嵌套 (nesting)、混合 (mixin)
- 对颜色和其它值进行操作的{Sass::Script::Functions 函数}
- 函数库[控制指令](http://sass.bootcss.com/docs/sass-reference/#control_directives)之类的高级功能
- 良好的格式，可对输出格式进行定制
- [支持 Firebug](https://addons.mozilla.org/en-US/firefox/addon/103988)

### 语法
###### 两种语法
- SCSS (Sassy CSS)，是一个 CSS3 语法的扩充版本，这份参考资料使用的就是此语法。 也就是说，所有符合 CSS3 语法的样式表也都是具有相同语法意义的 SCSS 文件。 另外，SCSS 理解大多数 CSS hacks 以及浏览器专属语法，例如[IE古老的 filter语法](http://msdn.microsoft.com/en-us/library/ms533754%28VS.85%29.aspx)。 这种语种语法的样式表文件需要以 .scss扩展名。
- Sass （缩排语法）， 提供了一种更简洁的 CSS 书写方式。 它不使用花括号，而是通过缩排的方式来表达选择符的嵌套层级，I 而且也不使用分号，而是用换行符来分隔属性。 很多人认为这种格式比 SCSS 更容易阅读，书写也更快速。 缩排语法具有 Sass 的所有特色功能， 虽然有些语法上稍有差异； 这些差异在{file:INDENTED_SYNTAX.md 所排语法参考手册}中都有描述。 使用此种语法的样式表文件需要以 .sass 作为扩展名

###### 两种语法相互转化

```
 //使用 sass-convert 命令行工具

 //将 Sass 转换为 SCSS
 sass-convert style.sass style.scss

 //将 SCSS 转换为 Sass
 sass-convert style.scss style.sass
```

### 使用 Sass
第一步安装 Sass gem：
```
gem install sass
```
如果你使用的是 Windows， 就需要先[安装 Ruby](http://rubyinstaller.org/download.html)。
如果要在命令行中运行 Sass ,只要输入
```
sass input.scss output.css
```
你还可以命令 Sass 监视文件的改动并更新 CSS ：
```
sass --watch input.scss:output.css
```
如果你的目录里有很多 Sass 文件，你还可以命令 Sass 监视整个目录：
```
sass --watch app/sass:public/stylesheets
```
使用 sass --help 可以列出完整的帮助文档。
SASS提供四个[编译风格](http://sass-lang.com/docs/yardoc/file.SASS_REFERENCE.html#output_style)的选项：
```
　　* nested：嵌套缩进的css代码，它是默认值。
　　* expanded：没有缩进的、扩展的css代码。
　　* compact：简洁格式的css代码。
　　* compressed：压缩后的css代码。
```
生产环境当中，一般使用最后一个选项。
```
sass --style compressed test.sass test.css
```

### 基本用法
SASS的官方网站，提供了一个[在线转换器](http://sass-lang.com/try.html)。可以进行练习。
##### 1 变量
SASS允许使用变量
- 支持六种主要的数据类型：
- 数字（例如 1.2、13、10px）
- 文本字符串，无论是否有引号（例如 "foo"、'bar'、baz）
- 颜色（例如 blue、#04a3f9、rgba(255, 0, 0, 0.5)）
- 布尔值（例如 true、false）
- 空值（例如 null）
- 值列表，用空格或逗号分隔（例如 1.5em 1em 0 2em、Helvetica, Arial, sans-serif）

SassScript 还支持所有其他 CSS 属性值类型， 例如 Unicode 范围和 !important 声明。 然而，它不会对这些类型做特殊处理。 它们只会被当做不带引号的字符串看待。

```
  //所有变量以$开头
$width: 5em;

#main {
  width: $width;
}
```
编译后
```
#main {
  width: 5em;
}
```
如果变量需要镶嵌在字符串之中，就必须需要写在#{}之中。
```
　　$side : left;
　　.rounded {
　　　　border-#{$side}-radius: 5px;
　　}
```
#####  2 运算

支持数字的标准运算（加 +、减 -、乘 *、除 /和取模 %）,数字也支持关系运算（<、>、<=、>=）， 等式运算（==、!=）被所有数据类型支持。
```
p {
  font: 10px/8px;             // 纯 CSS，不是除法运算
  $width: 1000px;
  width: $width/2;            // 使用了变量，是除法运算
  width: round(1.5)/2;        // 使用了函数，是除法运算
  height: (500px/2);          // 使用了圆括号，是除法运算
  margin-left: 5px + 8px/2px; // 使用了加（+）号，是除法运算
}
```
编译后
```
p {
  font: 10px/8px;
  width: 500px;
  height: 250px;
  margin-left: 9px; 
}
```
###### 2.1 颜色运算
所有算数运算都支持颜色值， 并且是分段运算的。 也就是说，红、绿、蓝各颜色分量会单独进行运算。 例如：
```
p {
  color: #010203 + #040506;
}
```
编译后
```
p {
  color: #050709; }
```
##### 3 CSS扩展嵌套
###### 3.1选择器嵌套
```
div{
  div1{
    color:$blue;
  }
}
```
###### 3.2属性嵌套
```

p{
  border:{
    color:$red;
  };
}
```
###### 3.3嵌套的代码块内，可以使用&引用父元素。比如a:hover伪类
```
a{
  color:$blue;
  &:hover{
    color:$red;
  }
}
```
编译后
```
a {
  color: blue;
}
a:hover {
  color: red;
}
```
#####  4 代码的复用
###### 4.1继承
```
.class1{
  padding:20px;
  margin:30px;
}
.class2{
  @extend .class1;
  font-size:16px;
}
```
编译后
```
.class1, .class2 {
  padding: 20px;
  margin: 30px;
}

.class2 {
  font-size: 16px;
}
```
###### 4.2 Mixin代码块, 有点像C语言的宏（macro），可以重用
Mixins允许您定义可以在整个样式表中重新使用的样式
```
//使用mixin指令 声明代码块
@mixin mixin1 {
  float:left;
  margin-right:10px;
}
@mixin mixin2($val : 10px){
  float:left;
  margin-right:$val;
}
//使用include指令 引用代码块
.div-mixin1{
  @include mixin1;
}
.div-mixin2{
  @include mixin2(20px);
}
```
###### 4.3 自定义函数
```
@function fun3($val){
  @return $val * 2 px;
}

.func-ex{
  padding:fun3(10);
}
```
编译后
```
.func-ex {
  padding: 20 px;
}
```
##### 5 逻辑判断
###### 5.1 if else
```
p{
  @if (1+2==4) {
    color:red;
  }@else{
    color:blue;
  }
}
```
###### 5.2 for循环
```
.for-ex{
  @for $i from 1 to 10 {
    .item#{$i}{
      color:$blue;
    }
  }
}
```
编译后
```
.for-ex .item1 {
  color: #000000;
}
.for-ex .item2 {
  color: #000000;
}
.for-ex .item3 {
  color: #000000;
}
.for-ex .item4 {
  color: #000000;
}
.for-ex .item5 {
  color: #000000;
}
.for-ex .item6 {
  color: #000000;
}
.for-ex .item7 {
  color: #000000;
}
.for-ex .item8 {
  color: #000000;
}
.for-ex .item9 {
  color: #000000;
}
```
###### 5.3 each循环
```
@each $animal in puma, sea-slug, egret, salamander {
  .#{$animal}-icon {
    background-image: url('/images/#{$animal}.png');
  }
}
```
编译后
```

.puma-icon {
  background-image: url("/images/puma.png");
}

.sea-slug-icon {
  background-image: url("/images/sea-slug.png");
}

.egret-icon {
  background-image: url("/images/egret.png");
}

.salamander-icon {
  background-image: url("/images/salamander.png");
}
```

##### 6 引入文件 及 注释
###### 6.1 引入文件
```
@import "css/index.css";
```
###### 6.2 注释
- 单行注释 ,只保留在SASS源文件中，编译后被省略
- 标准的CSS注释 ，会保留到编译后的文件
- 重要注释！ 即使是压缩模式编译，也会保留这行注释，通常可以用于声明版权信息
```
// 单行注释 
/*标准的CSS注释 */
/*! 重要注释！*/
```

完整的案例：[https://github.com/xiedajian/jsGrocery/blob/master/Sass%2CScss-demo/index.scss](https://github.com/xiedajian/jsGrocery/blob/master/Sass%2CScss-demo/index.scss)       

编译后：[https://github.com/xiedajian/jsGrocery/blob/master/Sass%2CScss-demo/index.css](https://github.com/xiedajian/jsGrocery/blob/master/Sass%2CScss-demo/index.css)       

参考:       

[阮一峰老师的SASS用法指南](http://www.ruanyifeng.com/)        

[SASS官方参考手册](http://sass.bootcss.com/docs/sass-reference/)       
