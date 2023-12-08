---
layout: archive
title: "Research"
permalink: /research/
author_profile: true
---

{% if author.googlescholar %}
  You can also find my articles on <u><a href="{{author.googlescholar}}">my Google Scholar profile</a>.</u>
{% endif %}

{% include base_path %}

<div><h1> Publications </h1></div>
<hr style="border-color:black;">
{% for post in site.research reversed %}
  {% if post.status == 'published' %}
    {% include archive-single.html %}
  {% endif %}
{% endfor %}

<div><h1> Working Papers </h1> </div>
<hr style="border-color:black;">
{% for post in site.research reversed %}
  {% if post.status == 'working' %}
    {% include archive-single.html %}
  {% endif %}
{% endfor %}
