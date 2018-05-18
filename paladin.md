---
layout: class
title: Paladin
permalink: paladin.html
---

## Paladin non-stance skills

{% for skill in site.data.paladin.non_stance_skills %}
  {% include skill.html %}
{% endfor %}
