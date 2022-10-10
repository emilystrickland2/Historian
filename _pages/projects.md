---
title: 
layout: default
permalink: https://emilystrickland2.github.io/Historian/projects/
published: true
---


<div class="ProjectContainer">

	<div class="gallery">


  {% for project in site.projects %}

  {% if project.redirect %}
  <div class="projectTile">
          <a href="{{ project.redirect }}" target="https://emilystrickland2.github.io/Historian/projects/">
          <span>
              <h2>{{ project.title }}</h2>
              <br/>
              <p>{{ project.description }}</p>
          </span>
          </a>
  </div>

  {% else %}

  <div class="projectTile">
          <a href="{{ https://emilystrickland2.github.io/Historian/projects/ | prepend: https://emilystrickland2.github.io/Historian/ | prepend: https://emilystrickland2.github.io/Historian/ }}">
          <span>
              <h2>{{ project.title }}</h2>
              <br/>
              <p>{{ project.description }}</p>
          </span>
          </a>
  </div>

  {% endif %}

  {% endfor %}

	</div>

</div>
