---
layout: default
title: Seminars
organizers: Dongchen Li, Jialun Li, Ronggang Shi, Ruxi Shi              # ← 在这里填写当前组织者；可随时修改
---

<h2>Seminars</h2>

{%- comment -%} 计算当前库里实际存在的年份（含已发生与未来） {%- endcomment -%}
{% assign all_sorted = site.seminars | sort: "datetime" %}
{% assign grouped = all_sorted | group_by_exp: "e", "e.datetime | date: '%Y'" %}
{% assign years = grouped | map: "name" | sort | reverse %}

{%- if years and years.size > 0 -%}
  <nav class="year-nav" style="margin: 0.75rem 0 1.25rem 0;">
    <strong style="margin-right: .5rem;">Years:</strong>
    {%- for y in years -%}
      <a href="/seminars/by-year.html?y={{ y }}" style="margin-right: .5rem; text-decoration: none;">
        {{ y }}
      </a>
    {%- endfor -%}
  </nav>
{%- endif -%}


<p>Current organizers: {% if page.organizers %}{{ page.organizers }}{% endif %}</p>

{% assign items = site.seminars | sort: "datetime" %}
{% assign now_ts = site.time | date: "%s" %}

<h3>Upcoming seminars</h3>
<ul class="seminar-list">
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
{% if aff_cn %}{% if aff_join != "" %}{% assign aff_join = aff_join | append: " " %}{% endif %}{% assign aff_join = aff_join | append: aff_cn %}{% endif %}
<li>
<div class="seminar-item-title"><strong>{{ s.title }}</strong></div>
<div class="seminar-item-meta">{{ name_line }}{% if aff_join != "" %} ({{ aff_join }}){% endif %}</div>
<div class="seminar-item-meta">{{ s.datetime | date: "%Y-%m-%d (%a) %H:%M" }}{% if s.place %} — {{ s.place }}{% endif %}</div>
{% if s.abstract %}<div class="seminar-item-abs"><strong>Abstract</strong>: {{ s.abstract }}</div>{% endif %}
</li>
{% assign future_printed = future_printed | plus: 1 %}
{% endif %}
{% endfor %}
{% if future_printed == 0 %}<li>No upcoming seminars.</li>{% endif %}
</ul>

{% assign groups = items | group_by_exp: "s", "s.datetime | date: '%Y'" %}
{% assign groups = groups | sort: "name" | reverse %}

{% for g in groups %}
{% assign printed = 0 %}
{% for s in g.items %}
{% assign s_ts = s.datetime | date: "%s" %}
{% if s_ts < now_ts %}
{% if printed == 0 %}
<h3>{{ g.name }}</h3>
<ul class="seminar-list">
{% endif %}
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
{% if s.abstract %}<div class="seminar-item-abs"><strong>Abstract</strong>: {{ s.abstract }}</div>{% endif %}
</li>
{% assign printed = printed | plus: 1 %}
{% endif %}
{% endfor %}
{% if printed > 0 %}</ul>{% endif %}
{% endfor %}
