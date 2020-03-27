---
layout: page
title: 카테고리
permalink: /category.html
ref: category
order: 2
---

<div id="archives">
{% for category in site.categories %}
  <div class="archive-group">
    {% capture category_name %}{{ category | first }}{% endcapture %}
    <div id="#{{ category_name | slugize }}"></div>
    <p></p>

    <h2 class="category-head">{{ category_name }}</h2>
    <a name="{{ category_name | slugize }}"></a>
    {% for post in site.categories[category_name] %}
    <article class="archive-item">
      {% if post.title.size >= 80 %}
        <li><a href="{{ site.baseurl }}{{ post.url }}">{{post.title | slice: 0, 80}}...</a></li>
      {% endif %}
      {% if post.title.size < 80 %}
        <li><a href="{{ site.baseurl }}{{ post.url }}">{{post.title}}</a></li>
      {% endif %}
    </article>
    {% endfor %}
  </div>
{% endfor %}
</div>