# 欢迎来到我的[个人博客](<https://yhb-flydream.github.io/>)

## 概览

- [效果预览](#效果预览)
- [Fork 指南](#fork-指南)
- [贴心提示](#贴心提示)
- [经验与思考](#经验与思考)
- [致谢](#致谢)

## 效果预览

**[在线预览 &rarr;](https://yhb-flydream.github.io/)**

![screenshot home](/images/blog-sreen.png)

## Fork 指南

> Fork 本项目之后，还需要做一些事情才能让你的页面「正确」跑起来。

- 正确设置项目名称与分支。
  - 按照 GitHub Pages 的规定，名称为 `username.github.io` 的项目的 master 分支，或者其它名称的项目的 gh-pages 分支可以自动生成 GitHub Pages 页面。

- 修改域名。
  - 如果你需要绑定自己的域名，那么修改 CNAME 文件的内容；如果不需要绑定自己的域名，那么删掉 CNAME 文件。

- 修改配置。
  - 网站的配置基本都集中在 \_config.yml 文件中，将其中与个人信息相关的部分替换成你自己的，比如网站的 title、subtitle 和 Disqus 的用户名等。
  - **注意：** 因为 Disqus 处理用户名与域名白名单的策略存在缺陷，请一定将 disqus\_username 修改成你自己的。我对该缺陷的记录见 [Issues#2][3]。

- 删除我的文章与图片。
  - 如下文件夹中除了 template.md 文件外，都可以全部删除，然后添加你自己的内容。
    - `\_posts` 文件夹中是我已发布的博客文章。
    - `\_drafts` 文件夹中是我尚未发布的博客文章。
    - `\_wiki` 文件夹中是我已发布的 wiki 页面。
    - `images` 文件夹中是我的文章和页面里使用的图片。

- 修改「关于」页面。
  - pages/about.md 文件内容对应网站的「关于」页面，里面的内容多为个人相关，将它们替换成你自己的信息，包括 \_data 目录下的 skills.yml 和 social.yml 文件里的数据。

## 贴心提示

- 排版建议遵照一定的规范，推荐 [中文文案排版指北（简体中文版）][1]。
- 在本地预览博客效果可以参考 [Setting up your Pages site locally with Jekyll][2]。

## 经验与思考

## 致谢

本博客外观基于 [DONGChuan](http://dongchuan.github.io) 修改，感谢！

[1]: https://github.com/mzlogin/chinese-copywriting-guidelines
[2]: https://help.github.com/articles/setting-up-your-pages-site-locally-with-jekyll/
[3]: https://github.com/mzlogin/mzlogin.github.io/issues/2
