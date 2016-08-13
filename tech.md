---
layout: page
title: Tech
permalink: /tech/
---


  <ul class="post-list">
    {{site.tags}}
    {% for post in site.tags.tech %}
      <li>
        <h2>
          <a class="post-link" href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a>
        </h2>
      </li>
    {% endfor %}
  </ul>
