---
layout: default
title: People
---

<h2>People</h2>

{% assign all = site.data.people.people | sort: "name" %}
{% assign wanted = "Faculty|Postdocs|Students" | split: "|" %}

{% for role in wanted %}
  {%- comment -%} 兼容把 Students 拼成 Studends {%- endcomment -%}
  {% if role == "Students" %}
    {% assign g1 = all | where: "role", "Students" %}
    {% assign g2 = all | where: "role", "Studends" %}
    {% assign group = g1 | concat: g2 %}
  {% else %}
    {% assign group = all | where: "role", role %}
  {% endif %}

  {% if group and group.size > 0 %}
  <section class="people-section">
    <h3>{{ role }}</h3>
    <div class="people-grid">
      {% assign group_sorted = group | sort: "name" %}
      {% for person in group_sorted %}
        <div class="person">
          {% if person.photo %}
            <img src="{{ person.photo | relative_url }}" alt="{{ person.name }}" class="avatar">
          {% endif %}
          <div class="name">
            {{ person.name }}{% if person.name_cn %} {{ person.name_cn }}{% endif %}
          </div>
          {% if person.email %}<div><a href="mailto:{{ person.email }}">{{ person.email }}</a></div>{% endif %}
          {% if person.website %}<div><a href="{{ person.website }}">Website</a></div>{% endif %}
        </div>
      {% endfor %}
    </div>
  </section>
  {% endif %}
{% endfor %}

{%- comment -%} 其他（未标 role 或不同拼写） {%- endcomment -%}
{% assign others = all | where_exp: "p", "p.role != 'Faculty' and p.role != 'Postdocs' and p.role != 'Students' and p.role != 'Studends'" %}
{% if others and others.size > 0 %}
  <section class="people-section">
    <h3>Others</h3>
    <div class="people-grid">
      {% assign others_sorted = others | sort: "name" %}
      {% for person in others_sorted %}
        <div class="person">
          {% if person.photo %}
            <img src="{{ person.photo | relative_url }}" alt="{{ person.name }}" class="avatar">
          {% endif %}
          <div class="name">
            {{ person.name }}{% if person.name_cn %} {{ person.name_cn }}{% endif %}
          </div>
          {% if person.email %}<div><a href="mailto:{{ person.email }}">{{ person.email }}</a></div>{% endif %}
          {% if person.website %}<div><a href="{{ person.website }}">Website</a></div>{% endif %}
        </div>
      {% endfor %}
    </div>
  </section>
{% endif %}
