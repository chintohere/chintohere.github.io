---
layout: page
title: Chinto's Blog 
tagline: Can you get something out of nothing.. 
---
{% include JB/setup %}

<blockquote>
Hi, I'm Kishore and I love programming, learning and using different technologies and building awesome web applications.  
Here is my attempt at jotting down things that might be usefull or not....
</blockquote>

## All Posts 

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>


