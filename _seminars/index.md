---
layout: default
title: Seminars
---

<h2>Seminars by Month</h2>
{% assign sorted = site.seminars | sort: "datetime" %}
{% assign groups = sorted | group_by_exp:"s","s.datetime | date: '%Y-%m'" %}
{% for g in groups %}
  <h3>{{ g.name }}</h3>
  <ul>
  {% for s in g.items %}
    <li><a href="{{ s.url }}">{{ s.title }}</a> — {{ s.speaker }} ({{ s.datetime | date: "%Y-%m-%d" }})</li>
  {% endfor %}
  </ul>
{% endfor %}
