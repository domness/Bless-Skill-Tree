---
layout: class
title: Paladin
permalink: paladin.html
---

## Paladin non-stance skills

{% for skill in site.data.paladin.non_stance_skills %}
  {% include skill.html %}
{% endfor %}

## Stances

{% for stance in site.data.paladin.stances %}
<div class='stance'>
<div class='stance-name'><h3>{{ stance.name }}</h3></div>

<ul class='stance-skills'>
{% assign skills = site.data.paladin[stance.slug] | where: "initial", true %}
{% for skill in skills %}
  <li>{% include skill.html %}
    <ul class='start'>{% include combo.html comboskill=skill %}</ul>
  </li>
{% endfor %}
</ul>

{% endfor %}
</div>
