---
layout: default
title: People
---

<h2>People</h2>

<div class="people-grid">
{% assign people_sorted = site.data.people.people | sort: "name" %}
{% for person in people_sorted %}
  <div class="person">
    {% if person.photo %}
      <img src="{{ person.photo | relative_url }}" alt="{{ person.name }}" class="avatar">
    {% endif %}
    <strong>{{ person.name }}</strong><br/>
    {% if person.role %}{{ person.role }}<br/>{% endif %}
    {% if person.email %}<a href="mailto:{{ person.email }}">{{ person.email }}</a><br/>{% endif %}
    {% if person.website %}<a href="{{ person.website }}">Website</a><br/>{% endif %}
  </div>
{% endfor %}
</div>
