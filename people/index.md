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
    <div class="name">{{ person.name }}</div>
    {% if person.role %}<div class="role">{{ person.role }}</div>{% endif %}
    {% if person.email %}<div><a href="mailto:{{ person.email }}">{{ person.email }}</a></div>{% endif %}
    {% if person.website %}<div><a href="{{ person.website }}">Website</a></div>{% endif %}
  </div>
{% endfor %}
</div>
