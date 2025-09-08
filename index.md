---
layout: default
title: Home
---

<h2>Upcoming Seminar</h2>
{% assign next_seminar = site.seminars | where_exp: "s","s.datetime >= 'now'" | sort: "datetime" | first %}
{% if next_seminar %}
<p><a href="{{ next_seminar.url }}"><strong>{{ next_seminar.title }}</strong></a> — {{ next_seminar.speaker }}</p>
<p><em>{{ next_seminar.datetime | date: "%Y-%m-%d %H:%M" }}</em></p>
{% else %}
<p>No upcoming seminar.</p>
{% endif %}

<h2>Upcoming Event</h2>
{% assign next_event = site.events | where_exp: "e","e.datetime >= 'now'" | sort: "datetime" | first %}
{% if next_event %}
<p><a href="{{ next_event.url }}"><strong>{{ next_event.title }}</strong></a></p>
<p><em>{{ next_event.datetime | date: "%Y-%m-%d %H:%M" }}</em></p>
{% else %}
<p>No upcoming event.</p>
{% endif %}
