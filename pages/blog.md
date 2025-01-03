---
layout: page
title: Blog
permalink: /blog/
---

<div class="blog-index">
  {% assign sorted_posts = site.posts | sort: 'date' | reverse %}
  {% for post in sorted_posts %}
    <article class="post-preview">
      <h2 class="post-title">
        <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
      </h2>
      
      <div class="post-meta">
        <span class="post-date">{{ post.date | date: "%B %d, %Y" }}</span>
        {% if post.author %}
          <span class="post-author">by {{ post.author }}</span>
        {% endif %}
      </div>

      {% if post.tags %}
        <div class="post-tags">
          {% for tag in post.tags %}
            <span class="tag">{{ tag }}</span>
          {% endfor %}
        </div>
      {% endif %}

      <div class="post-excerpt">
        {{ post.excerpt }}
      </div>
    </article>
    <hr>
  {% else %}
    <p>Debug info:</p>
    <ul>
      <li>Posts directory: {{ site.posts_dir }}</li>
      <li>Number of posts: {{ site.posts.size }}</li>
      <li>Collections dir: {{ site.collections_dir }}</li>
    </ul>
    <p>No posts found. Make sure posts are in content/posts/ directory.</p>
  {% endfor %}
</div> 