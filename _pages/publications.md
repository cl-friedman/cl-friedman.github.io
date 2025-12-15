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

<!-- Safety Check: Flatten bibliography if grouped by year in config -->

{% if raw_bib %}
{% assign is_grouped = false %}

<!-- Check if the first item looks like a group (has 2 elements, second is array) -->

{% if raw_bib.first.size == 2 %}
{% assign is_grouped = true %}
{% endif %}

{% if is_grouped %}
<!-- It is grouped by year (hash), so we flatten it into a list -->
{% for year_group in raw_bib %}
{% assign all_papers = all_papers | concat: year_group[1] %}
{% endfor %}
{% else %}
<!-- It is already a flat list -->
{% assign all_papers = raw_bib %}
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
<!-- This calls _includes/bib.liquid to render the entry -->
{% include bib.liquid %}
{% endfor %}
</div>
{% endfor %}

<!-- 2. Talks Section (Rendered Separately at Bottom) -->

<!-- Initialize empty array to prevent concat errors -->

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
