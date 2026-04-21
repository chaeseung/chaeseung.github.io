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

{% comment %} 1. 카테고리가 0개인 포스트들만 미리 골라냅니다 {% endcomment %}
{% assign uncategorized_posts = site.posts | where_exp: "item", "item.categories.size == 0" %}

{% comment %} 2. 만약 해당 포스트가 하나라도 있다면 섹션을 출력합니다 {% endcomment %}
{% if uncategorized_posts.size > 0 %}
  <hr>
  <h2 id="uncategorized">Uncategorized</h2>
  <ul>
    {% for post in uncategorized_posts %}
      <li>
        <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
        <span class="post-meta"> - {{ post.date | date: "%Y-%m-%d" }}</span>
      </li>
    {% endfor %}
  </ul>
{% endif %}
