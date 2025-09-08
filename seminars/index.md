---
layout: default
title: Seminars
---

## Seminars (All)

{% assign items = site.seminars | sort: "datetime" %}
{% assign current_year = "" %}
{% for s in items %}
{% assign y = s.datetime | date: "%Y" %}
{% if y != current_year %}
### {{ y }}
{% assign current_year = y %}
{% endif %}

- **{{ s.title }}** — {{ s.speaker }}{% if s.affiliation %} ({{ s.affiliation }}){% endif %}
  - {{ s.datetime | date: "%Y-%m-%d (%a) %H:%M" }}{% if s.place %} — {{ s.place }}{% endif %}
  {% if s.abstract %}
  - {{ s.abstract }}
  {% endif %}

{% endfor %}