# yhb-flydream

> 欢迎来访问我的[个人博客](https://yhb-flydream.github.io/)
> 本博客外观基于[码志的博客](http://mazhuang.org/)修改

## 介绍

- [项目目录介绍](#项目目录介绍)
- [效果预览](#效果预览)
- [Fork 说明](#fork-说明)
- [贴心提示](#贴心提示)
- [经验与思考](#经验与思考)

## 项目目录介绍
- `_data` 
  - `links.yml` 可以添加友链
  - `skills.yml` 添加技能标签(展示于**关于**页面)
  - `social.yml` 添加社交账号(展示于**关于**页面)
- `_drafts` 文件夹中是我尚未发布的博客文章。
- `_includes` 文件夹中是页面分块
- `_layouts` 文件夹中是项目的所有页面
- `_posts` 文件夹中是我已发布的博客文章。
- `_storelib`
  - `me.html` 我的简历
- `_wiki` 文件夹中是我已发布的github的 wiki 页面。
- `assets` 本项目的样式、图片和js
- `images` 文件夹中是我的文章和页面里使用的图片。
- `page`
  - `404.md` 404页面
  - `about.md` 关于页面内容
  - `categories.md` 分类页面内容
  - `links.md` 友链页面内容
  - `me.md` 简历页面内容
  - `open-source.md` 开源项目内容
  - `wiki.md` wiki页面内容
- `_config.yml` 网站的配置项
- `favicon.ico` 图标
- `index.html` 首页内容
- `README.md` README文件


## 效果预览

**[在线预览 &rarr;](https://yhb-flydream.github.io/)**

![screenshot home](/images/blog-sreen.png)

## Fork 说明

> Fork 本项目之后，还需要做一些事情才能让你的页面「正确」跑起来。

- 正确设置项目名称与分支。
  - 按照 GitHub Pages 的规定，名称为 `username.github.io` 的项目的 master 分支，或者其它名称的项目的 gh-pages 分支可以自动生成 GitHub Pages 页面。

- 修改域名。
  - 如果你需要绑定自己的域名，那么修改 CNAME 文件的内容；如果不需要绑定自己的域名，那么删掉 CNAME 文件。

- 修改配置。
  - 网站的配置基本都集中在 `_config.yml` 文件中，将其中与个人信息相关的部分替换成你自己的，比如网站的 title、subtitle 和 Disqus 的用户名等。
  - **注意：** 因为 Disqus 处理用户名与域名白名单的策略存在缺陷，请一定将 `disqus_username` 修改成你自己的。我对该缺陷的记录见 [Issues#2][3]。

```
# ---------------- #
#   Main Configs   #
# ---------------- #
baseurl:                               # 为项目名，若项目是'***.github.io'，则设置为空''
url: https://yhb-flydream.github.io    # 个人网站地址
date_format: "ordinal"                 # 
title: yhb-flydream                    # 博客名称（可以用github用户名）
subtitle:                              # 博客正文大标题
description:                           # 描述（可以写自己擅长的技术）
keywords:                              # 关键词（可以写自己擅长的技术）
favicon: /favicon.ico                  # 图标（位置在根目录）
timezone: China/Zhengzhou              # 时区
encoding: "utf-8"
side_bar_repo_limit: 5

# ---------------- #
#      Author      #
# ---------------- #
author: yhb-flydream                   # 作者名称
organization:                          # 所在公司名称
organization_url:                      # 网站地址
github_username: yhb-flydream          # 可以用github用户名
location: Zhengzhou, China             # 所在地区
email: yhbflydream@gmail.com           # 个人邮箱

# ---------------- #
#      Jekyll      #
# ---------------- #
markdown: kramdown
kramdown:
   input: GFM
highlighter: rouge
paginate: 8
lsi: false
quiet: false
excerpt_separator: "\n\n"
permalink: /:year/:month/:day/:title/
gems:
   - jekyll-github-metadata
   - rouge
#     - jekyll-html-pipeline
   - jekyll-paginate
   - jekyll-sitemap
   - jekyll-feed
   - jemoji
#     - jekyll-mentions
collections:
   wiki:
       output: true
       permalink: /wiki/:path/
repository: yhb-flydream.github.io     # 自己博客地址

# ---------------- #
#    Navigation    #
# ---------------- #                   # 页面右侧导航
navs:
-
  href: /
  label: 首页

-
  href: /categories/
  label: 分类

-
  href: /wiki/
  label: 收藏

-
  href: /about/
  label: 关于

-
  href: /me/
  label: 简历

# ---------------- #
#      Comments    #
# ---------------- #
# support provider: disqus, netease_gentie, gitment 支持的评论平台（disqus, netease_gentie, gitment）
comments_provider: gitment

# !!!重要!!! 请修改下面这些信息为你自己申请的
# !!!Important!!! Please modify infos below to yours

# 可以去访问 https://disqus.com 注册账号，把账号名写下面
disqus_username: yhbflydream
**注意：** 因为 Disqus 处理用户名与域名白名单的策略存在缺陷，请一定将 disqus.username 修改成你自己的。

# 可以去访问 https://gentie.163.com 注册账号，把key写下面
# netease_gentie_key: 560ed243b708465d82d5a0a5f3b83da1

# 可以去访问 https://imsun.net/posts/gitment-introduction/ 注册账号，把需要的信息写下面
gitment:
   owner: yhbflydream                  # 自己的github ID
   repo: yhb-flydream.github.io        # 自己的项目名
   oauth:                              # 自己的OAuth
       client_id: 4d061788eeaabef903b8
       client_secret: 8b323f24d7f51b0fa30a5396b43edfc369352619
**注意：** 在注册OAuth的时候，Authorization callback URL务必是博客主页地址

# 在使用其它评论组件时可点击显示 Disqus
```
- 注册OAuth的注意事项

> ![213](/images/blog/2017-07-08_1.png)
> ![213](/images/blog/2017-07-08_2.png)
> ![213](/images/blog/2017-07-08_3.png)

- 删除我的文章与图片。如下文件夹中除了 `template.md` 文件外，都可以全部删除或修改，然后添加你自己的内容。

  - `\_drafts` 文件夹中是我尚未发布的博客文章。
  - `\_posts` 文件夹中是我已发布的博客文章。（可以全部删除，写你自己的内容）
  - `\_wiki` 文件夹中是我已发布的github的 wiki 页面。
  - `images` 文件夹中是我的文章和页面里使用的图片。

- 修改「关于」页面。
  - pages/about.md 文件内容对应网站的「关于」页面，里面的内容多为个人相关，将它们替换成你自己的信息，包括 \_data 目录下的 skills.yml 和 social.yml 文件里的数据。

## 贴心提示

- 排版建议遵照一定的规范，推荐 [中文文案排版指北（简体中文版）][1]。
- 在本地预览博客效果可以参考 [Setting up your Pages site locally with Jekyll][2]。

## 经验与思考


[1]: https://github.com/mzlogin/chinese-copywriting-guidelines
[2]: https://help.github.com/articles/setting-up-your-pages-site-locally-with-jekyll/
[3]: https://github.com/mzlogin/mzlogin.github.io/issues/2
