---
layout: default
title: People
---

<h2>People</h2>
{% assign grouped = site.data.people.people | group_by_exp:"p","p.name | slice:0,1" %}
{% for g in grouped %}
<h3>{{ g.name }}</h3>
<div style="display:flex;flex-wrap:wrap;gap:10px;">
  {% for person in g.items %}
    <div style="flex:1 0 18%;border:1px solid #ccc;padding:5px;box-sizing:border-box;">
      <strong>{{ person.name }}</strong><br/>
      {% if person.role %}{{ person.role }}<br/>{% endif %}
      {% if person.email %}<a href="mailto:{{ person.email }}">{{ person.email }}</a><br/>{% endif %}
      {% if person.website %}<a href="{{ person.website }}">Website</a><br/>{% endif %}
    </div>
  {% endfor %}
</div>
{% endfor %}
