---
title: Adding Categories on Jekyll
date: 2021-03-18 09:52:00 +08:00
categories: Web Design
---

This site was built using Jekyll. While I usually prefer to use no-code tools like Webflow (I have sooo much love for Webflow), I wanted to practice coding on my own site. Now, Jekyll is awesome, but if you need to use categories in your site, the feature doesn't come by default and there's some additional steps involved.

There are already tons of tutorials for how to do this online, but it seems none of them were updated except for [Azure Patterns](https://www.azurepatterns.com/2020/03/11/jekyll-categories)'s one. When I tried it, however, the code doesn't close the for tag.

So I thought I'd share my own steps:

1. Create a layout for your category pages. Save it as **category.html** to your **_layouts** folder.

\`---
layout: default

---

<div class="categories">
<h1 class="category-title">Topic: {{ page.category-name }}</h1>
<div class="posts">
{% for post in site.categories\[page.category-name\] %}
<div class="post">
<p class="post-meta">
{% if site.date_format %}
{{ post.date | date: site.date_format }}
{% else %}
{{ post.date | date: "%b %-d, %Y" }}
{% endif %}
</p>
<a href="{{ post.url | relative_url }}" class="post-link">
<h3 class="post-title">
{{ post.title }}
</h3>
</a>
<span class="post-summary">
{{ post.excerpt }}
</span>
</div>
{%- endfor -%}
</div>
</div>\`

2\.  Make a category page for every category. Save this to your root folder. Important: **category-name** is case-sensitive.

`--- layout: category
category-name: digital marketing
permalink: "/category/digitalmarketing" ---`