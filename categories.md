---
layout: page
title: Categories
permalink: /categories/
---

{% assign sorted_categories = site.categories | sort %}

{% for category in sorted_categories %}
  <h2 id="{{ category[0] | slugify }}">{{ category[0] }}</h2>
  <ul>
    {% for post in category[1] %}
      <li>
        <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
        <span class="post-meta"> - {{ post.date | date: "%Y-%m-%d" }}</span>
      </li>
    {% endfor %}
  </ul>
{% endfor %}

<hr>

<h2 id="uncategorized">Uncategorized</h2>
<ul>
  {% assign has_uncategorized = false %}
  {% for post in site.posts %}
    {% if post.categories.size == 0 %}
      <li>
        <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
        <span class="post-meta"> - {{ post.date | date: "%Y-%m-%d" }}</span>
      </li>
      {% assign has_uncategorized = true %}
    {% endif %}
  {% endfor %}

  {% if has_uncategorized == false %}
    <li>모든 포스트가 분류되었습니다.</li>
  {% endif %}
</ul>
