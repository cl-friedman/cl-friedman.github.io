---
layout: page 
permalink: /publications/
title: publications 
description: publications by categories in reversed chronological order 
nav: true 
nav_order: 3
---

<!-- Get all papers -->
{% assign raw_bib = site.scholar.bibliography %}
{% assign all_papers = "" | split: "" %}

{% if raw_bib %}
  <!-- Safety Check: Handle both Grouped-by-Year (default) and Flat bibliographies -->
  {% if raw_bib.first.title %}
    <!-- It has a title property, so it is already a flat list of papers -->
    {% assign all_papers = raw_bib %}
  {% else %}
    <!-- It is a grouped hash (e.g. by year), so we must flatten it -->
    {% for year_group in raw_bib %}
       {% assign year_papers = year_group[1] %}
       {% if year_papers %}
         {% assign all_papers = all_papers | concat: year_papers %}
       {% endif %}
    {% endfor %}
  {% endif %}
{% endif %}

<!-- Group by Category -->
{% assign publications_by_category = all_papers | group_by: 'category' %}

<!-- 1. Main Publications Loop (Skipping "Talk" entries) -->
{% for category in publications_by_category %}
  {% assign cat_name = category.name %}
  
  <!-- Skip Talk/Talks here; we render them later -->
  {% if cat_name == 'Talk' or cat_name == 'Talks' %}
    {% continue %}
  {% endif %}
  
  <h2 class="bibliography mt-4">{{ cat_name }}</h2>
  <div class="publications">
    {% for entry in category.items %}
      <!-- EXPLICITLY pass the entry variable to the include -->
      {% include bib.liquid entry=entry %}
    {% endfor %}
  </div>
{% endfor %}

<!-- 2. Talks Section (Rendered Separately at Bottom) -->
<!-- We filter both variants ('Talk' and 'Talks') and render sequentially -->
{% assign talk_entries = all_papers | where: "category", "Talk" %}
{% assign talks_plural = all_papers | where: "category", "Talks" %}

<!-- Check if we have any talks to show -->
{% assign show_talks = false %}
{% if talk_entries.size > 0 or talks_plural.size > 0 %}
  {% assign show_talks = true %}
{% endif %}

{% if show_talks %}
  <h2 class="bibliography mt-4">Talks</h2>
  <div class="publications">
    <!-- Render 'Talk' entries -->
    {% for entry in talk_entries %}
      {% include bib.liquid entry=entry %}
    {% endfor %}
    
    <!-- Render 'Talks' entries -->
    {% for entry in talks_plural %}
      {% include bib.liquid entry=entry %}
    {% endfor %}
  </div>
{% endif %}
