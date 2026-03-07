---
layout: post
title: "如何在github上搭建个人博客(Jekyll)"
date: 2026-03-07
categories: [学习]
tags: [git, markdown]
---

- 前言：为了防止自己忘记如何上传文章的各种细节操作，所以第一篇笔记用来记录如何在github上搭建起自己的博客。

> 0x01 建立仓库

在拥有github账号之后。

- 点击右上角 `+` → `New repository`。
- **Repository name** 填写 `my-blog`（或其他名字）。
- 选择 Public（公开）或 Private（私有，但 Pages 仅限公开仓库免费使用）。
- 勾选 **Add a README file**（方便立即克隆）。
- 点击 **Create repository**。

> 0x02 几个关键文件

GitHub Pages 原生支持 Jekyll，可以方便地用 Markdown 写文章。

1.在仓库根目录下创建一个 `_config.yml` 文件，内容至少包含：

```yaml
title: 我的博客
theme: jekyll-theme-cayman  # 选择一个官方主题，也可用 minima
```

2.创建 `_posts` 文件夹，在里面放你的文章，**命名格式必须是** `YYYY-MM-DD-标题.md`，日期和标题之间用短横线连接，不能有空格。例如 `2025-01-01-hello-world.md`。

3.提交这些文件，稍后访问博客就能看到文章列表（取决于主题）。这就是访问链接

```text
https://k0e1.github.io/2025/01/01/hello-world/
```

*注意：标题部分取自文件名中的 `hello-world`（不含日期），且末尾通常带斜杠 `/`。*

> 0x03 文章内容注意事项

在 Jekyll 博客中，每篇文章不一定必须包含 Front Matter，但强烈建议添加，其格式为

```yaml
---
layout: post
title: "你的文章标题"
date: 2026-03-07
categories: [分类]
tags: [标签1, 标签2]
---
这里是文章正文，用 Markdown 格式写...
```

> 0x04 git本地上传

**1.本地写文章**

```bash
cd xxx.github.io
cd _posts
# 创建新文章文件
touch 2026-03-07-git-tutorial.md
```

**2.推送到 GitHub**

```bash
git add .
git commit -m "新增 xxx 教程文章"
git push origin main
```

**3.线上查看**

等待 1-2 分钟，访问 `https://xxx.github.io/2026/03/07/git-tutorial/` 确认发布成功。

> 0x05 其它

**1.如何添加文章列表到首页**

- 在仓库根目录找到 `readme.md`。
- 添加以下内容来动态显示所有文章：

```
---
layout: default
title: 我的博客
---

# 文章列表

下面是一段用于显示文章列表的 Liquid 代码：
{% raw %}
<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
      <span>{{ post.date | date: "%Y-%m-%d" }}</span>
    </li>
  {% endfor %}
</ul>
{% endraw %}
```

**2.如何添加文章页的上一篇/下一篇导航**

修改文章页面的布局文件（通常是 `_layouts/post.html`），在其中添加上一页和下一页的链接。

1. 在仓库根目录创建 `_layouts` 文件夹（如果不存在）。
2. 在该文件夹内创建 `post.html` 文件。
3. 将以下内容写入 `post.html`：

```
---
layout: default
---
{% raw %}
<h1>{{ page.title }}</h1>
<p>{{ page.date | date: "%Y-%m-%d" }}</p>

<div>
  {{ content }}
</div>

<!-- 上一篇/下一篇导航 -->
<div style="margin-top: 2em;">
  {% if page.previous %}
    <a href="{{ page.previous.url | relative_url }}">← 上一篇：{{ page.previous.title }}</a>
  {% endif %}
  {% if page.next %}
    <a href="{{ page.next.url | relative_url }}" style="float: right;">下一篇：{{ page.next.title }} →</a>
  {% endif %}
</div>
{% endraw %}
```

ok,至此结束第一篇文章的，可能有很多考虑不全的地方，今后慢慢改进。