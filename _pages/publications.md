---
layout: page 
permalink: /publications/
title: publications 
description: publications by categories in reversed chronological order 
nav: true 
nav_order: 3
---

{% assign raw_bib = site.scholar.bibliography %}
{% assign all_papers = "" | split: "" %}

{% if raw_bib %}
  {% assign is_grouped = false %}
  
  {% if raw_bib.first.size == 2 %}
    {% assign is_grouped = true %}
  {% endif %}

  {% if is_grouped %}
    {% for year_group in raw_bib %}
       {% assign all_papers = all_papers | concat: year_group[1] %}
    {% endfor %}
  {% else %}
    {% assign all_papers = raw_bib %}
  {% endif %}
{% endif %}

{% assign publications_by_category = all_papers | group_by: 'category' %}

{% for category in publications_by_category %}
  {% assign cat_name = category.name %}
  
  {% if cat_name == 'Talk' or cat_name == 'Talks' %}
    {% continue %}
  {% endif %}
  
  <h2 class="bibliography mt-4">{{ cat_name }}</h2>
  <div class="publications">
    {% for entry in category.items %}
      {% include bib.liquid %}
    {% endfor %}
  </div>
{% endfor %}

{% assign empty_array = "" | split: "" %}

{% assign talk_entries = all_papers | where: "category", "Talk" %}
{% unless talk_entries %}
  {% assign talk_entries = empty_array %}
{% endunless %}

{% assign talks_plural = all_papers | where: "category", "Talks" %}
{% unless talks_plural %}
  {% assign talks_plural = empty_array %}
{% endunless %}

{% assign all_talks = talk_entries | concat: talks_plural %}

{% if all_talks.size > 0 %}
  <h2 class="bibliography mt-4">Talks</h2>
  <div class="publications">
    {% for entry in all_talks %}
      {% include bib.liquid %}
    {% endfor %}
  </div>
{% endif %}
