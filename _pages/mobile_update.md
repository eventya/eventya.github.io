---
layout: page
title: Mobile Updates
permalink: /mobile_updates/
---

<ul>
  {% for post in site.posts %}
    <li>
      <span>{{ post.date | date: "%b %-d, %Y" }}</span>
      <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
      <p>Categories: {{ post.categories | jsonify }}</p>
      <p>{{ post.content | markdownify | strip_html | truncatewords: 30 }}</p>
    </li>
  {% endfor %}
</ul>
