---
layout: default
title: Home
---

{% assign future_seminars = site.seminars 
  | where_exp: "s", "s.datetime | date: '%s' >= site.time | date: '%s'" 
  | sort: "datetime" %}
{% assign next_seminar = future_seminars | first %}

{% if next_seminar %}
  <p><a href="{{ next_seminar.url }}"><strong>{{ next_seminar.title }}</strong></a> — {{ next_seminar.speaker }}</p>
  <p><em>{{ next_seminar.datetime | date: "%Y-%m-%d %H:%M" }}</em></p>
{% else %}
  <p>No upcoming seminar.</p>
{% endif %}

{% assign future_events = site.events 
  | where_exp: "e", "e.datetime | date: '%s' >= site.time | date: '%s'" 
  | sort: "datetime" %}
{% assign next_event = future_events | first %}

{% if next_event %}
  <p><a href="{{ next_event.url }}"><strong>{{ next_event.title }}</strong></a></p>
  <p><em>{{ next_event.datetime | date: "%Y-%m-%d %H:%M" }}</em></p>
{% else %}
  <p>No upcoming event.</p>
{% endif %}
