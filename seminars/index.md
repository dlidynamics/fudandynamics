---
layout: default
title: Seminars
---

<h2>Seminars (All)</h2>

{% assign items = site.seminars | sort: "datetime" %}
{% assign current_year = "" %}
{% for s in items %}
  {% assign y = s.datetime | date: "%Y" %}
  {% if y != current_year %}
    {% unless forloop.first %}</ul>{% endunless %}
    <h3>{{ y }}</h3>
    <ul>
    {% assign current_year = y %}
  {% endif %}

  <li style="margin:.6rem 0;">
    <div><strong>{{ s.title }}</strong> — {{ s.speaker }}{% if s.affiliation %} ({{ s.affiliation }}){% endif %}</div>
    <div style="opacity:.8;">
      {{ s.datetime | date: "%Y-%m-%d (%a) %H:%M" }}{% if s.place %} — {{ s.place }}{% endif %}
    </div>
    {% if s.abstract %}
      <div style="margin-top:.3rem;">{{ s.abstract }}</div>
    {% endif %}
  </li>
{% endfor %}
{% if items and items.size > 0 %}</ul>{% endif %}