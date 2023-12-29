---
layout: post
title: Mobile Applications Updates
date: 2000-01-31 12:00:00 +0300
permalink: /mobile_updates/
---

<ul>
  {% for post in site.pages %}
    {% if post.title contains 'Mobile version' %}
    <li>
      <h3><a class="post-link" href="{{ post.url }}">{{ post.title }}</a></h3>
    </li>
    {% endif %}
  {% endfor %}
</ul>
