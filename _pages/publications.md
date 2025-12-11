---
layout: page
permalink: /publications/
title: publications
description: publications by categories in reversed chronological order
nav: true
nav_order: 1
---

<!-- Custom Grouping Loop -->
{% assign publications_by_category = site.scholar.bibliography | group_by: 'category' %}

{% for category in publications_by_category %}
  <h2 class="bibliography mt-4">{{ category.name }}</h2>
  <div class="publications">
    {% for entry in category.items %}
      {% include bib.liquid %}
    {% endfor %}
  </div>
{% endfor %}
