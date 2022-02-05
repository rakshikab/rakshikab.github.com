---
layout: page
title: Google Summer of Code '16
permalink: /gsoc16/
---

# These are my weekly logs from my Google Summer of Code 2016 project with BRL-CAD.

{% assign weeks = site.gsoc16 | sort: "week" %}
{% for week in weeks %}
  <h2>
    <a href="{{ week.url }}">
      {{ week.title }}
    </a>
  </h2>
{% endfor %}