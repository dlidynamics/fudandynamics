---
layout: default
title: Events
---

## Events (All)

{% assign items = site.events | sort: "datetime" %}
{% assign current_year = "" %}
{% for e in items %}
{% assign y = e.datetime | date: "%Y" %}
{% if y != current_year %}
### {{ y }}
{% assign current_year = y %}
{% endif %}

- **{{ e.title }}**
  - {{ e.datetime | date: "%Y-%m-%d (%a) %H:%M" }}{% if e.place %} — {{ e.place }}{% endif %}
  {% if e.description %}
  - {{ e.description }}
  {% endif %}

{% endfor %}