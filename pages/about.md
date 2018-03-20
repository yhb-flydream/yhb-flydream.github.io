---
layout: page
title: 我的简介
description: 我的简介
keywords: 我的简介
comments: true
menu: 关于
permalink: /about/
---


## 找到我

{% for website in site.data.social %}
* {{ website.sitename }}：[@{{ website.name }}]({{ website.url }})
{% endfor %}

## 我的特长

{% for category in site.data.skills %}
### {{ category.name }}
<div class="btn-inline">
{% for keyword in category.keywords %}
<button class="btn btn-outline" type="button">{{ keyword }}</button>
{% endfor %}
</div>
{% endfor %}

> {% for category in site.data.skills %}{% for keyword in category.keywords %}{{ keyword }} {% endfor %}{% endfor %}
