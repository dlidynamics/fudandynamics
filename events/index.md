---
layout: default
title: Events
---

<h2>Events by Month</h2>
{% assign sorted = site.events | sort: "datetime" %}
{% assign groups = sorted | group_by_exp:"e","e.datetime | date: '%Y-%m'" %}
{% for g in groups %}
  <h3>{{ g.name }}</h3>
  <ul>
  {% for e in g.items %}
    <li><a href="{{ e.url }}">{{ e.title }}</a> ({{ e.datetime | date: "%Y-%m-%d" }})</li>
  {% endfor %}
  </ul>
{% endfor %}
