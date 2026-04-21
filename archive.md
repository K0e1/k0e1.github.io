---
layout: default # 先创建 _layouts/default.html 基础布局
title: 文章归档
---
<link rel="stylesheet" href="{{ "/assets/css/style.css" | relative_url }}">

# 文章归档
<div class="archive-container">
  {% assign posts_by_year = site.posts | group_by_exp: "post", "post.date | date: '%Y'" %}
  {% for year in posts_by_year %}
    <h2>{{ year.name }} 年</h2>
    {% assign posts_by_month = year.items | group_by_exp: "post", "post.date | date: '%m'" %}
    {% for month in posts_by_month %}
      <h3>{{ month.name }} 月</h3>
      <ul class="archive-list">
        {% for post in month.items %}
          <li>
            <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
            <span>{{ post.date | date: "%Y-%m-%d" }}</span>
          </li>
        {% endfor %}
      </ul>
    {% endfor %}
  {% endfor %}
</div>

<style>
/* 归档页面专属样式（补充到 style.css 也可） */
.archive-container {
  margin-top: 2rem;
}
.archive-list {
  grid-template-columns: 1fr; /* 归档列表单列展示 */
  margin-left: 1rem;
}
h3 {
  color: #7928ca;
  margin-top: 1rem;
  margin-left: 0.5rem;
}
</style>