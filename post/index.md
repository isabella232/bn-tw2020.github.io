---
layout: default
title: "post"
description: 기술 및 회고
main: true
project-header: true
header-img: img/about.jpg
draft: true
---

<ul class="catalogue">
{% assign sorted = site.pages | sort: 'order' | reverse %}
{% for page in sorted %}
{% if page.post == true %}
{% include post-list.html %}
{% endif %}
{% endfor %}
</ul>