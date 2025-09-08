---
layout: default
title: Home
---

## Upcoming Seminar
{% assign now_ts = site.time | date: "%s" %}
{% assign next_seminar = nil %}
{% assign sorted_sems = site.seminars | sort: "datetime" %}
{% for s in sorted_sems %}
  {% assign s_ts = s.datetime | date: "%s" %}
  {% if s_ts >= now_ts %}
    {% assign next_seminar = s %}
    {% break %}
  {% endif %}
{% endfor %}
{% if next_seminar %}

**{{ next_seminar.title }}**

{%- comment -%} 名字 + 中文名（可选） {%- endcomment -%}
{%- assign name_line = next_seminar.speaker -%}
{%- if next_seminar.speaker_cn -%}
  {%- assign name_line = name_line | append: " " | append: next_seminar.speaker_cn -%}
{%- endif -%}

{%- comment -%} 单位：英文/中文均可选，至少一个才加括号 {%- endcomment -%}
{%- assign aff_en = next_seminar.affiliation | default: next_seminar.affliation -%}
{%- assign aff_cn = next_seminar.affiliation_cn -%}
{%- if aff_en or aff_cn -%}
  {%- assign aff_join = "" -%}
  {%- if aff_en -%}{%- assign aff_join = aff_en -%}{%- endif -%}
  {%- if aff_cn -%}{%- assign aff_join = aff_join | append: " " | append: aff_cn -%}{%- endif -%}
  {{ name_line }} ({{ aff_join }})
{%- else -%}
  {{ name_line }}
{%- endif %}

*{{ next_seminar.datetime | date: "%Y-%m-%d (%a) %H:%M" }}{% if next_seminar.place %} — {{ next_seminar.place }}{% endif %}*

{% if next_seminar.abstract %}
  
**Abstract**: {{ next_seminar.abstract }}
{% endif %}
{% else %}
No upcoming seminar.
{% endif %}

---

## Upcoming Event
{% assign next_event = nil %}
{% assign sorted_events = site.events | sort: "datetime" %}
{% for e in sorted_events %}
  {% assign e_ts = e.datetime | date: "%s" %}
  {% if e_ts >= now_ts %}
    {% assign next_event = e %}
    {% break %}
  {% endif %}
{% endfor %}
{% if next_event %}
  **{{ next_event.title }}**  
  *{{ next_event.datetime | date: "%Y-%m-%d (%a) %H:%M" }}{% if next_event.place %} — {{ next_event.place }}{% endif %}*

  {% if next_event.description %}
  {{ next_event.description }}
  {% endif %}
{% else %}
  No upcoming event.
{% endif %}