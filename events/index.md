---
layout: default
title: Events
---

<h2>Events (All)</h2>

{% assign items = site.events | sort: "datetime" %}
{% assign current_year = "" %}
{% for e in items %}
  {% assign y = e.datetime | date: "%Y" %}
  {% if y != current_year %}
    {% unless forloop.first %}</ul>{% endunless %}
    <h3>{{ y }}</h3>
    <ul>
    {% assign current_year = y %}
  {% endif %}

  <li style="margin:.6rem 0;">
    <div><strong>{{ e.title }}</strong></div>
    <div style="opacity:.8;">
      {{ e.datetime | date: "%Y-%m-%d (%a) %H:%M" }}{% if e.place %} — {{ e.place }}{% endif %}
    </div>
    {% if e.description %}
      <div style="margin-top:.3rem;">{{ e.description }}</div>
    {% endif %}
  </li>
{% endfor %}
{% if items and items.size > 0 %}</ul>{% endif %}