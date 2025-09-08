---
layout: default
title: Seminars
organizers: Dongchen Li, Jialun Li, Ronggang Shi, Ruxi Shi              # ← 在这里填写当前组织者；可随时修改
---

<h2>Seminars</h2>
<p>Current organizers: {% if page.organizers %}{{ page.organizers }}{% endif %}</p>

<!-- 本页局部样式：控制条目间距与对齐 -->
<style>
  .seminar-list { margin: .4rem 0 1.2rem; padding-left: 1.25rem; }
  .seminar-list li { margin-bottom: 1.6rem; }         /* 两条之间“多空一行”的效果 */
  .seminar-item-title { font-weight: 700; }
  .seminar-item-meta { margin-left: 1rem; }           /* subbullet 两行右移一些 */
  .seminar-item-abs  { margin-top: .6rem; }           /* 摘要前空一行；与题目左对齐（不缩进） */
</style>

{% assign items = site.seminars | sort: "datetime" %}
{% assign groups = items | group_by_exp: "s", "s.datetime | date: '%Y'" %}

{% for g in groups %}
<h3>{{ g.name }}</h3>
<ol class="seminar-list">
{% for s in g.items %}
{% assign aff_en = s.affiliation | default: s.affliation %}
{% assign aff_cn = s.affiliation_cn %}
{% assign name_line = s.speaker %}
{% if s.speaker_cn %}{% assign name_line = name_line | append: " " | append: s.speaker_cn %}{% endif %}
{% assign aff_join = "" %}
{% if aff_en %}{% assign aff_join = aff_en %}{% endif %}
{% if aff_cn %}{% if aff_join != "" %}{% assign aff_join = aff_join | append: " " %}{% endif %}{% assign aff_join = aff_join | append: aff_cn %}{% endif %}

<li>
  <div class="seminar-item-title"><strong>{{ s.title }}</strong></div>
  <div class="seminar-item-meta">{{ name_line }}{% if aff_join != "" %} ({{ aff_join }}){% endif %}</div>
  <div class="seminar-item-meta">{{ s.datetime | date: "%Y-%m-%d (%a) %H:%M" }}{% if s.place %} — {{ s.place }}{% endif %}</div>
  {% if s.abstract %}
  <div class="seminar-item-abs">{{ s.abstract }}</div>
  {% endif %}
</li>

{% endfor %}
</ol>
{% endfor %}