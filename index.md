---
layout: page
title: Nagarjuna Kumar
tagline: Personal homepage
---
{% include JB/setup %}

## Hello!

I'm a software developer with a focus on big data analytics, machine learning and algorithm development, and have experience with large datasets and distributed computing systems.

I am currently based in the beautiful city of Cambridge, UK.


## Posts

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>



