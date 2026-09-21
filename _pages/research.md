---
layout: archive
title: "Research"
permalink: /research/
author_profile: true
---

{% if site.author.googlescholar %}
  <p class="academic-profile-link">You can also find my research on <a href="{{ site.author.googlescholar }}">Google Scholar</a>.</p>
{% endif %}

{% include base_path %}

<div class="academic-list research-list">
  <section class="academic-section" aria-labelledby="publications-heading">
    <h2 id="publications-heading" class="academic-section__title">Publications</h2>
    {% assign publication_items = site.research | where: "status", "published" | sort: "display_order" %}
    {% for post in publication_items %}
    {% include archive-single.html %}
    {% endfor %}
  </section>

  <section class="academic-section" aria-labelledby="working-papers-heading">
    <h2 id="working-papers-heading" class="academic-section__title">Working Papers</h2>
    {% assign working_items = site.research | where: "status", "working" | sort: "display_order" %}
    {% for post in working_items %}
    {% include archive-single.html %}
    {% endfor %}
  </section>
</div>
