---
layout: default
title: 主页
---

# k0e1.github.io

## 这是主页

<!-- 新增归档链接 -->
<p><a href="{{ "/archive.html" | relative_url }}" style="font-size: 1.1rem;">📁 文章归档</a></p>

# 文章列表
<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
      <span>{{ post.date | date: "%Y-%m-%d" }}</span>
    </li>
  {% endfor %}
</ul>