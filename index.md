---
layout: page
title: nagarjuna kumar
tagline: personal homepage
---
{% include JB/setup %}

## Hello there,
i am just `blog.testing()`
Nothing here is ready to be seen by

	anyone other than;
	me;

so yes

### Posts

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>



