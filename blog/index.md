---
layout: default
title: Blog
---

My ramblings, if you care to read them.

<ul class="posts">
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
      <span>{{ post.date | date_to_string }}</span>
      <p>{{ post.excerpt | remove: '<p>' | remove: '</p>' }}<code>...</code></p>
        </li>
  {% endfor %}
</ul>
