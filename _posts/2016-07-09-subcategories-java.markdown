---
layout: page
title:  "Java"
tags: tech
permalink: /tech/java/index
---

<ul class="post-list">
  {% for post in site.tags.java %}
    <li>
      <h2>
        <a class="post-link" href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a>
      </h2>
    </li>
  {% endfor %}
</ul>
