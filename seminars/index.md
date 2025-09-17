---
layout: default
title: Seminars
---

# Seminars

{% assign items = site.seminars | sort: "datetime" %}
{% assign now_ts = site.time | date: "%s" | plus: 0 %}

<!-- ===== Upcoming（默认展开） ===== -->
<details class="seminar-section" id="upcoming" open markdown="1">
  <summary>
    <h2 style="display:inline; margin:0;">Upcoming seminars</h2>
  </summary>

{% assign printed_upcoming = 0 %}
{% for s in items %}
  {% assign s_ts = s.datetime | date: "%s" | plus: 0 %}
  {% if s_ts >= now_ts %}

* **{{ s.title }}**
  {% assign name_line = s.speaker %}
  {% if s.speaker_cn %}{% assign name_line = name_line | append: " " | append: s.speaker_cn %}{% endif %}
  {% assign aff_en = s.affiliation | default: s.affliation %}
  {% assign aff_cn = s.affiliation_cn %}
  {% assign aff_join = "" %}
  {% if aff_en %}{% assign aff_join = aff_en %}{% endif %}
  {% if aff_cn %}{% if aff_join != "" %}{% assign aff_join = aff_join | append: " / " %}{% endif %}{% assign aff_join = aff_join | append: aff_cn %}{% endif %}
  {{ name_line }}{% if aff_join != "" %} ({{ aff_join }}){% endif %}<br>
  {{ s.datetime | date: "%Y-%m-%d (%a) %H:%M" }}{% if s.place %} — {{ s.place }}{% endif %}<br>
  **Abstract**{% if s.abstract %}: {{ s.abstract }}{% endif %}

  {% assign printed_upcoming = printed_upcoming | plus: 1 %}
  {% endif %}
{% endfor %}

{% if printed_upcoming == 0 %}
* **No upcoming seminars.**
{% endif %}
</details>

{% comment %}
  ====== 统计所有实际出现的年份（避免不稳定的 group_by_exp 写法）======
{% endcomment %}
{% assign year_str = "" %}
{% for s in items %}
  {% assign y = s.datetime | date: "%Y" %}
  {% unless year_str contains y %}
    {% if year_str == "" %}
      {% assign year_str = y %}
    {% else %}
      {% assign year_str = year_str | append: "," | append: y %}
    {% endif %}
  {% endunless %}
{% endfor %}
{% assign years = year_str | split: "," | sort | reverse %}

{% comment %}
  ====== 各年份（默认折叠，只显示已发生的）======
{% endcomment %}
{% for y in years %}
  {% assign count = 0 %}
  {% for s in items %}
    {% assign y2 = s.datetime | date: "%Y" %}
    {% assign s_ts = s.datetime | date: "%s" | plus: 0 %}
    {% if y2 == y and s_ts < now_ts %}
      {% assign count = count | plus: 1 %}
    {% endif %}
  {% endfor %}

  {% if count > 0 %}
<details class="seminar-year" id="year-{{ y }}" markdown="1">
  <summary>
    <h2 style="display:inline; margin:0;">{{ y }}</h2>
  </summary>

{% for s in items %}
  {% assign y2 = s.datetime | date: "%Y" %}
  {% assign s_ts = s.datetime | date: "%s" | plus: 0 %}
  {% if y2 == y and s_ts < now_ts %}

* **{{ s.title }}**
  {% assign name_line = s.speaker %}
  {% if s.speaker_cn %}{% assign name_line = name_line | append: " " | append: s.speaker_cn %}{% endif %}
  {% assign aff_en = s.affiliation | default: s.affliation %}
  {% assign aff_cn = s.affiliation_cn %}
  {% assign aff_join = "" %}
  {% if aff_en %}{% assign aff_join = aff_en %}{% endif %}
  {% if aff_cn %}{% if aff_join != "" %}{% assign aff_join = aff_join | append: " / " %}{% endif %}{% assign aff_join = aff_join | append: aff_cn %}{% endif %}
  {{ name_line }}{% if aff_join != "" %} ({{ aff_join }}){% endif %}<br>
  {{ s.datetime | date: "%Y-%m-%d (%a) %H:%M" }}{% if s.place %} — {{ s.place }}{% endif %}<br>
  **Abstract**{% if s.abstract %}: {{ s.abstract }}{% endif %}

  {% endif %}
{% endfor %}

</details>
  {% endif %}
{% endfor %}

<style>
/* 折叠区的轻量样式（不改变你的 Markdown 列表格式） */
.seminar-section, .seminar-year { margin: 0 0 1rem 0; }
.seminar-section > summary, .seminar-year > summary {
  cursor: pointer;
  list-style: none;
  padding: .4rem .6rem;
  border-radius: .5rem;
  background: rgba(0,0,0,.04);
}
.seminar-section[open] > summary, .seminar-year[open] > summary {
  background: rgba(0,0,0,.06);
}
.seminar-section > summary::-webkit-details-marker,
.seminar-year > summary::-webkit-details-marker { display: none; }
</style>
