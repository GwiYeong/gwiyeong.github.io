---
layout: page
title:  "Python"
tags: tech
permalink: /tech/python/index
---

<ul class="post-list">
  {% for post in site.tags.python %}
    <li>
      <h2>
        <a class="post-link" href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a>
      </h2>
    </li>
  {% endfor %}
</ul>
