---
layout: base
---

# Tags

<ul>
{% for page in site.pages %}
  {% if forloop.last %}
    <a href="{{ site.baseurl }}/{{ page.url }}">└ {{ page.title }}</a><br>
  {% else %}
    <a href="{{ site.baseurl }}/{{ page.url }}">├ {{ page.title }}</a><br>
  {% endif %}
{% endfor %}
</ul>
