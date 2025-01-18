---
layout: default
title: blog
permalink: /blog/
---

<style>
  .blog-index {
    max-width: 800px;
    margin: 0 auto;
    padding: 20px;
  }

  .post-preview {
    margin-bottom: 2rem;
    padding: 1rem 0;
  }

  .post-title {
    margin-bottom: 0.5rem;
  }

  .post-title a {
    text-decoration: none;
    color: var(--primary);
    transition: color 0.2s ease;
  }

  .post-title a:hover {
    color: var(--primary-hover);
  }

  .post-meta {
    font-size: 0.9rem;
    color: #666;
    margin-bottom: 1rem;
  }

  .post-author {
    margin-left: 1rem;
  }

  .post-tags {
    margin-top: 0.5rem;
  }

  .tag {
    display: inline-block;
    background-color: #f0f0f0;
    padding: 0.2rem 0.8rem;
    border-radius: 15px;
    font-size: 0.8rem;
    color: #666;
    margin-right: 0.5rem;
    margin-bottom: 0.5rem;
  }

  hr {
    border: none;
    border-top: 1px solid #eee;
    margin: 2rem 0;
  }
</style>

<div class="blog-index">
  {% assign sorted_posts = site.posts | sort: 'date' | reverse %}
  {% assign last_post_date = sorted_posts.first.date %}

  {% for post in sorted_posts %}
    <article class="post-preview">
      <h3 class="post-title" >
        <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
      </h3>
      
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
    </article>
    <hr>
  {% else %}
    <p>No posts found. Make sure posts are in content/posts/ directory.</p>
  {% endfor %}
</div> 
