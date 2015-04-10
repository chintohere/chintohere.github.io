---
layout: page
title: Kishore Chintoju 
tagline: Father, Husband, Programmer and a Lifelong Learner
---
{% include JB/setup %}

<blockquote>
Hi, I'm Kishore and I love making things. Programming is one of my faviourite tools. I love learning and using different technologies and building awesome web applications.  
</blockquote>

## Recent posts*(or not so recent)* 
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
