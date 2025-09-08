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
  {% assign aff = next_seminar.affiliation | default: next_seminar.affliation %}
**{{ next_seminar.title }}**  
{{ next_seminar.speaker }}{% if next_seminar.speaker_cn %} {{ next_seminar.speaker_cn }}{% endif %}  
*{{ next_seminar.datetime | date: "%Y-%m-%d (%a) %H:%M" }}{% if next_seminar.place %} — {{ next_seminar.place }}{% endif %}*
{% if aff %} ({{ aff }}){% endif %}

{% if next_seminar.abstract %}
{{ next_seminar.abstract }}
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