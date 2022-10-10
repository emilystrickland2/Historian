---
title: 
layout: default
permalink: https://emilystrickland2.github.io/Historian/blog/
published: true
---

<div class="BlogContainer">

    <div class="gallery">

  {% blog in site.blogs %}

  {% if blog.redirect %}
  <div class="BlogTile">
          <a href="{{ blog.redirect }}" target="_blank">
          <span>
              <h2>{{ blog.title }}</h2>
              <br/>
              <p>{{ blog.description }}</p>
          </span>
          </a>
  </div>

  {% else %}

  <div class="blogTile">
          <a href="{{ https://emilystrickland2.github.io/Historian/blog/ | prepend: https://emilystrickland2.github.io/Historian/ | prepend: https://emilystrickland2.github.io/Historian/ }}">
          <span>
              <h2>{{ blog.title }}</h2>
              <br/>
              <p>{{ blog.description }}</p>
          </span>
          </a>
  </div>

  {% endif %}

  {% endfor %}

    </div>

</div>
