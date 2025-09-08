---
layout: default
title: People
---

<h2>People</h2>

{% assign all = site.data.people.people | sort: "name" %}
{% assign roles = "Faculty|Postdocs|Students" | split: "|" %}

{%- comment -%}
依次输出三个分组。为避免 where_exp 解析问题，不用复杂筛选，
而是在每个分组里遍历 all，命中即输出。
{%- endcomment -%}
{% for role in roles %}
  {% assign printed = 0 %}
  {% for person in all %}
    {% assign r = person.role | default: "" %}
    {% if r == role or (role == "Students" and r == "Studends") %}
      {% if printed == 0 %}
        <section class="people-section">
          <h3>{{ role }}</h3>
          <div class="people-grid">
      {% endif %}
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
      {% assign printed = printed | plus: 1 %}
    {% endif %}
  {% endfor %}
  {% if printed > 0 %}
          </div>
        </section>
  {% endif %}
{% endfor %}

{%- comment -%}
最后输出 Others：role 不在三组里的都归到这里
{%- endcomment -%}
{% assign printed_others = 0 %}
{% for person in all %}
  {% assign r = person.role | default: "" %}
  {% if r != "Faculty" and r != "Postdocs" and r != "Students" and r != "Studends" %}
    {% if printed_others == 0 %}
      <section class="people-section">
        <h3>Others</h3>
        <div class="people-grid">
    {% endif %}
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
    {% assign printed_others = printed_others | plus: 1 %}
  {% endif %}
{% endfor %}
{% if printed_others > 0 %}
        </div>
      </section>
{% endif %}
