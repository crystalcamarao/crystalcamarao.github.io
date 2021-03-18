---
title: 2 Steps to Adding Category Pages on Jekyll
date: 2021-03-18 10:13:00 +08:00
categories:
- web design
tags:
- jekyll
---

This site was built using Jekyll. While I usually prefer to use no-code tools like Webflow (I have sooo much love for Webflow), I wanted to practice coding on my own site. Now, Jekyll is awesome, but if you need to use categories in your site, the feature doesn't come by default and there's some additional steps involved.

There are already tons of tutorials for how to do this online, but it seems none of them were updated except for [Azure Patterns](https://www.azurepatterns.com/2020/03/11/jekyll-categories)'s one. When I tried it, however, the code doesn't close the **for** tag.

So I thought I'd share my own steps:

1. Create a layout for your category pages. Save it as **category.html** to your **_layouts** folder.
<pre><code>

---

## layout: default

<div class="categories">
<h2 class="category-title">
Topic: {{ page.category-name }}
</h2>
<div class="posts">
<ul class="post-list">
{%- assign date_format = site.minima.date_format | default: "%b %-d, %Y" -%}
{% for post in site.categories\[page.category-name\] %}
<li>
<span class="post-meta">{{ post.date | date: date_format }}</span>
<h3>
<a class="post-link" href="{{ post.url | relative_url }}">
{{ post.title | escape }}
</a>
</h3>
{%- if site.show_excerpts -%}
{{ post.excerpt }}
{%- endif -%}
</li>
{%- endfor -%}
</ul>
</div>
</div>
</code></pre>

2\. Make a category page for every category. Save this to your root folder.
{% raw %}

---

permalink: "/category/digitalmarketing"
layout: category
category-name: digital marketing

---

{% endraw %}

3\. BONUS (Optional): List and link to each category.
{% raw %}
<h3 class="category-topic">Topics</h3>
<ul>
{% assign sortedCategories = site.categories | sort %}
{% for category in sortedCategories %}
{% assign cat4url = category\[0\] | remove:' ' | downcase %}
<li><a class="category-item" href="{{site.baseurl}}/category/{{cat4url}}">
{{category\[0\]}}
</a>
</li>
{% endfor %}
</ul>
{% endraw %}

4\. BONUS (Optional): Show the categories of each post by pasting this in the **post.html** layout page.
{% raw %}
<div class="post-categories">
{% if post %}
{% assign categories = post.categories %}
{% else %}
{% assign categories = page.categories %}
{% endif %}
{% for category in categories %}
<a href="{{site.baseurl}}/category/{{category|remove:' '| downcase}}">{{category}}</a>
{% unless forloop.last %} {% endunless %}
{% endfor %}
</div>
{% endraw %}

And that's it. Happy Jekyll-ing!