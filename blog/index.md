---
layout: page
title: Chinto's Blog 
tagline: Can you get something out of nothing... 
---
{% include JB/setup %}

<blockquote>
This is my attempt to note down things I found useful and were not already out there at the time of writing. They are not limited to any topic. Hopefully they will benefit someone.
</blockquote>

## Recent posts
<div class="home">

  <div class="posts">
    {% for post in site.posts limit:10 %}
      <div class="post">
          <p class="post-meta">{{ post.date | date: "%b %-d, %Y" }}</p>
            <a href="{{ post.url | prepend: site.baseurl }}" class="post-link">
                <h3 class="h3 post-title">{{ post.title }}</h3>
            </a>        
        <p class="post-summary">
            {% if post.summary %}
              {{ post.summary }}
            {% else %}
              {{ post.excerpt }}
            {% endif %}
          </p>
      </div>
    {% endfor %}
  </div>

</div>

## All Posts 

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>


