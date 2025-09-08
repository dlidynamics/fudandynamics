---
layout: default
title: Seminars
organizers: Dongchen Li, Jialun Li, Ronggang Shi, Ruxi Shi              # ← 在这里填写当前组织者；可随时修改
---

## Seminars
Current organizers: {% if page.organizers %}{{ page.organizers }}{% endif %}

{% assign items = site.seminars | sort: "datetime" %}
{% assign groups = items | group_by_exp: "s", "s.datetime | date: '%Y'" %}

{% for g in groups %}
### {{ g.name }}

{% for s in g.items %}
{% assign aff_en = s.affiliation | default: s.affliation %}
{% assign aff_cn = s.affiliation_cn %}
{% assign name_line = s.speaker %}
{% if s.speaker_cn %}{% assign name_line = name_line | append: " " | append: s.speaker_cn %}{% endif %}

{{ forloop.index }}. **{{ s.title }}**
   - {{ name_line }}{% if aff_en or aff_cn %} ({% if aff_en %}{{ aff_en }}{% endif %}{% if aff_en and aff_cn %} {{ aff_cn }}{% elsif aff_cn %}{{ aff_cn }}{% endif %}){% endif %}
   - {{ s.datetime | date: "%Y-%m-%d (%a) %H:%M" }}{% if s.place %} — {{ s.place }}{% endif %}

{% if s.abstract %}
   **Abstract**: {{ s.abstract }}
{% endif %}

{% unless forloop.last %}
<br/>
{% endunless %}
{% endfor %}

{% endfor %}