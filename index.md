---
layout: base
---
## [遊戲列表](./Game/)
## Tags分類
<ul>
  {% assign game_pages = site.pages | where_exp: "page", "page.url contains '/Game/'" %}
  
  {% assign all_tags = "" | split: "" %}
  {% for page in game_pages %}
    {% if page.tags %}
      {% assign page_tags = page.tags | join: ',' | split: ',' %}
      {% assign all_tags = all_tags | concat: page_tags %}
    {% endif %}
  {% endfor %}
  {% assign unique_tags = all_tags | uniq | sort %}
  
  {% for tag in unique_tags %}
    <li><strong>{{ tag }}</strong>
    {% assign tag_pages = game_pages | where_exp: "page", "page.tags contains tag" %}
    {% assign index_pages = "" | split: "" %}
    {% for page in tag_pages %}
      {% unless page.url contains 'proposal' or page.url contains 'analysis' %}
        {% assign index_pages = index_pages | push: page %}
      {% endunless %}
    {% endfor %}

    <ul>
      {% for page in index_pages %}
        <li>
          <a href="{{ page.url | relative_url }}">
            {% if forloop.last %}└{% else %}├{% endif %}
            {{ page.title | default: page.name }}
          </a>
        </li>
      {% endfor %}
    </ul>
    </li>
  {% endfor %}
</ul>