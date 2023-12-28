---
layout: default
title: Mobile Updates
permalink: /mobile_updates/
---

<ul>
  {% for post in site.posts %}
    {% if post.title contains 'Mobile version' %}
      <li>
        <h3><a class="post-link" href="{{ post.url }}">{{ post.title }}</a></h3>
      </li>
    {% endif %}
  {% endfor %}
</ul>
