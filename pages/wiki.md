---
layout: page
title: Wiki
description: 学习是一条令人时而欣喜若狂、时而郁郁寡欢的旅途。
keywords: 维基, Wiki
comments: false
menu: 维基
permalink: /wiki/
---

> 学习是一条令人时而欣喜若狂、时而郁郁寡欢的旅途。I Want Something Just Like This.

<ul class="listing">
{% for wiki in site.wiki %}
{% if wiki.title != "Wiki Template" %}
<li class="listing-item"><a href="{{ wiki.url }}">{{ wiki.title }}</a></li>
{% endif %}
{% endfor %}
</ul>
