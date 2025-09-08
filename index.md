---
layout: default
title: Home
---

<h2>Upcoming Seminar</h2>
{% assign now_ts = site.time | date: "%s" %}
{% assign sorted_sems = site.seminars | sort: "datetime" %}
{% assign next_seminar = nil %}
{% for s in sorted_sems %}
  {% assign s_ts = s.datetime | date: "%s" %}
  {% if s_ts >= now_ts %}
    {% assign next_seminar = s %}
    {% break %}
  {% endif %}
{% endfor %}
{% if next_seminar %}
  <p>
    <a href="{{ next_seminar.url | relative_url }}"><strong>{{ next_seminar.title }}</strong></a>
    — {{ next_seminar.speaker }}
  </p>
  <p><em>{{ next_seminar.datetime | date: "%Y-%m-%d %H:%M" }}</em>{% if next_seminar.place %} — {{ next_seminar.place }}{% endif %}</p>
{% else %}
  <p>No upcoming seminar.</p>
{% endif %}

<h2>Upcoming Event</h2>
{% assign sorted_events = site.events | sort: "datetime" %}
{% assign next_event = nil %}
{% for e in sorted_events %}
  {% assign e_ts = e.datetime | date: "%s" %}
  {% if e_ts >= now_ts %}
    {% assign next_event = e %}
    {% break %}
  {% endif %}
{% endfor %}
{% if next_event %}
  <p><a href="{{ next_event.url | relative_url }}"><strong>{{ next_event.title }}</strong></a></p>
  <p><em>{{ next_event.datetime | date: "%Y-%m-%d %H:%M" }}</em>{% if next_event.place %} — {{ next_event.place }}{% endif %}</p>
{% else %}
  <p>No upcoming event.</p>
{% endif %}
