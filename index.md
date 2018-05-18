---
layout: default
title: Home
---

## Classes

<ul>
  {% for class in site.data.classes %}
    <li>
      {% if class.page %}
        <a href='{{ class.page }}.html'>{{ class.name }}</a>
      {% else %}
        {{ class.name }}
      {% endif %}    
    </li>
  {% endfor %}
</ul>

## Examples

### Paladin non-stance skills

{% for skill in site.data.paladin.non_stance_skills %}
  {% include skill.html %}
{% endfor %}

### Combo Tree

Coming soon...