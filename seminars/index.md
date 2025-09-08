---
layout: default
title: Seminars
---

## Seminars

{% assign items = site.seminars | sort: "datetime" %}
{% for s in items %}
{% assign aff_en = s.affiliation | default: s.affliation %}
{% assign aff_cn = s.affiliation_cn %}
{% assign name_line = s.speaker %}
{% if s.speaker_cn %}{% assign name_line = name_line | append: " " | append: s.speaker_cn %}{% endif %}

{{ forloop.index }}. **{{ s.title }}**
   - {{ name_line }}{% if aff_en or aff_cn %} ({% if aff_en %}{{ aff_en }}{% endif %}{% if aff_en and aff_cn %} {{ aff_cn }}{% elsif aff_cn %}{{ aff_cn }}{% endif %}){% endif %}
   - {{ s.datetime | date: "%Y-%m-%d (%a) %H:%M" }}{% if s.place %} — {{ s.place }}{% endif %}

{% if s.abstract %}
   {{ s.abstract }}
{% endif %}

{% if forloop.last == false %}

{% endif %}
{% endfor %}