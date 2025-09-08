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
    {% unless forloop.first %}</ul>{% endunless %}
    ### {{ y }}
    <ul>
    {% assign current_year = y %}
  {% endif %}

  {%- assign aff_en = s.affiliation | default: s.affliation -%}
  {%- assign aff_cn = s.affiliation_cn -%}
  {%- assign name_line = s.speaker -%}
  {%- if s.speaker_cn -%}
    {%- assign name_line = name_line | append: " " | append: s.speaker_cn -%}
  {%- endif -%}
  {%- assign aff_join = "" -%}
  {%- if aff_en -%}{%- assign aff_join = aff_en -%}{%- endif -%}
  {%- if aff_cn -%}{%- if aff_join != "" -%}{%- assign aff_join = aff_join | append: " " -%}{%- endif -%}{%- assign aff_join = aff_join | append: aff_cn -%}{%- endif -%}

  - **{{ s.title }}**
    - {{ name_line }}{% if aff_en or aff_cn %} ({{ aff_join }}){% endif %}
    - {{ s.datetime | date: "%Y-%m-%d (%a) %H:%M" }}{% if s.place %} — {{ s.place }}{% endif %}
    {% if s.abstract %}
    - {{ s.abstract }}
    {% endif %}
{% endfor %}
{% if items and items.size > 0 %}</ul>{% endif %}