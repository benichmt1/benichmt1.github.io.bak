---
layout: page
title: Hello World!
tagline: Supporting tagline
---
{% for post in site.posts offset: 0 limit: 50 %}
<div class="row">
<div class="span7">
<div class="row">
<div class="span2">
<a href="{{ post.url }}" >
<img border="0" width="250" height="150" src="/img/posts/{{ post.image }}" alt="">
</a>
</div>
<div class="span5">
<h4><strong><a href="{{ post.url }}">{{ post.title }}</a></strong></h4>
<p>
{{ post.summary }}
</p>
<p>
<i class="icon-calendar"></i> {{ post.date | date: "%B %e, %Y" }}
| <i class="icon-comment"></i> <a href="http://benichmt1.github.com{{ post.url }}#disqus_thread" data-disqus-identifier="{{ post.url }}"></a>
| <i class="icon-tags"></i> Tags :{% for tag in post.tags %} <a href="/tags/{{ tag }}" rel="tooltip" title="View posts tagged with &quot;{{ tag }}&quot;"><span class="label label-info">{{ tag }}</span></a> {% if forloop.last != true %} {% endif %} {% endfor %}
</p>
<p><a href="{{ post.url }}">Read more</a></p>
</div>
</div>
<hr>
</div>
</div>
{% endfor %}

{% include JB/setup %}

Read [Jekyll Quick Start](http://jekyllbootstrap.com/usage/jekyll-quick-start.html)

Complete usage and documentation available at: [Jekyll Bootstrap](http://jekyllbootstrap.com)

## Update Author Attributes

In `_config.yml` remember to specify your own data:
    
    title : My Blog =)
    
    author :
      name : Name Lastname
      email : blah@email.test
      github : username
      twitter : username

The theme should reference these variables whenever needed.
    
## Sample Posts

This blog contains sample posts which help stage pages and blog data.
When you don't need the samples anymore just delete the `_posts/core-samples` folder.

    $ rm -rf _posts/core-samples

Here's a sample "posts list".

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

## To-Do

This theme is still unfinished. If you'd like to be added as a contributor, [please fork](http://github.com/plusjade/jekyll-bootstrap)!
We need to clean up the themes, make theme usage guides with theme-specific markup examples.


