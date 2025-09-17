---
layout: default
title: Seminars
organizers: Dongchen Li, Jialun Li, Ronggang Shi, Ruxi Shi # ← 在这里填写当前组织者；可随时修改
---

## Seminars

Current organizers: {% if page.organizers %}{{ page.organizers }}{% endif %}

{% assign items = site.seminars | sort: "datetime" %}
{% assign now_ts = site.time | date: "%s" %}

<!-- Upcoming：默认展开 -->
<details class="seminar-section" id="upcoming" open markdown="1">
  <summary>
    <h3 style="display:inline; margin:0;">Upcoming seminars</h3>
  </summary>

{% assign future_printed = 0 %}
{% for s in items %}
  {% assign s_ts = s.datetime | date: "%s" %}
  {% if s_ts >= now_ts %}
    {% assign aff_en = s.affiliation | default: s.affliation %}
    {% assign aff_cn = s.affiliation_cn %}
    {% assign name_line = s.speaker %}
    {% if s.speaker_cn %}{% assign name_line = name_line | append: " " | append: s.speaker_cn %}{% endif %}

    {% assign aff_join = "" %}
    {% if aff_en %}{% assign aff_join = aff_en %}{% endif %}
    {% if aff_cn %}
      {% if aff_join != "" %}{% assign aff_join = aff_join | append: " " %}{% endif %}
      {% assign aff_join = aff_join | append: aff_cn %}
    {% endif %}

* {{ s.title }}

{{ name_line }}{% if aff_join != "" %} ({{ aff_join }}){% endif %}

{{ s.datetime | date: "%Y-%m-%d (%a) %H:%M" }}{% if s.place %} — {{ s.place }}{% endif %}

{% if s.abstract %}
Abstract: {{ s.abstract }}
{% endif %}

    {% assign future_printed = future_printed | plus: 1 %}
  {% endif %}
{% endfor %}

{% if future_printed == 0 %}
* No upcoming seminars.
{% endif %}
</details>

{% assign groups = items | group_by_exp: "s", "s.datetime | date: '%Y'" %}
{% assign groups = groups | sort: "name" | reverse %}

{% for g in groups %}
  {% assign printed = 0 %}
  {% for s in g.items %}
    {% assign s_ts = s.datetime | date: "%s" %}
    {% if s_ts < now_ts %}
      {% if printed == 0 %}
<!-- 年份区块：默认折叠 -->
<details class="seminar-year" id="year-{{ g.name }}" markdown="1">
  <summary>
    <h3 style="display:inline; margin:0;">{{ g.name }}</h3>
  </summary>
      {% endif %}

    {% assign aff_en = s.affiliation | default: s.affliation %}
    {% assign aff_cn = s.affiliation_cn %}
    {% assign name_line = s.speaker %}
    {% if s.speaker_cn %}{% assign name_line = name_line | append: " " | append: s.speaker_cn %}{% endif %}

    {% assign aff_join = "" %}
    {% if aff_en %}{% assign aff_join = aff_en %}{% endif %}
    {% if aff_cn %}
      {% if aff_join != "" %}{% assign aff_join = aff_join | append: " " %}{% endif %}
      {% assign aff_join = aff_join | append: aff_cn %}
    {% endif %}

* {{ s.title }}

{{ name_line }}{% if aff_join != "" %} ({{ aff_join }}){% endif %}

{{ s.datetime | date: "%Y-%m-%d (%a) %H:%M" }}{% if s.place %} — {{ s.place }}{% endif %}

{% if s.abstract %}
Abstract: {{ s.abstract }}
{% endif %}

      {% assign printed = printed | plus: 1 %}
    {% endif %}
  {% endfor %}

  {% if printed > 0 %}
</details>
  {% endif %}
{% endfor %}


