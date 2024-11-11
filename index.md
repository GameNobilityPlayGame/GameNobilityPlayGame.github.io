---
layout: base
---
## [遊戲列表](./Game/)
## Tags分類
<ul>
  {% assign game_pages = site.pages | where_exp: "page", "page.url contains '/Game/'" %}
  
  {% assign all_tags = "" %}
  {% for page in site.pages %}
    {% if page.tags %}
      {% assign all_tags = all_tags | concat: page.tags %}
    {% endif %}
  {% endfor %}

  {% assign unique_tags = all_tags | uniq %}
  
  {% for tag in unique_tags %}
    {{ tag }}
    <ul>
      {% assign tag_pages = game_pages | where_exp: "page", "page.tags contains tag" %}
      {% for page in tag_pages %}
        <a href="/{{ page.path | replace: " ", "%20" | remove: ".md" }}">
          {% if forloop.last %}└{% else %}├{% endif %}
          
          {{ page.title }}
          
          {% if page.url contains "proposal" %}
            一頁式提案
          {% elsif page.url contains "analysis" %}
            分析
          {% endif %}
          
        </a><br>
      {% endfor %}
    </ul>
  {% endfor %}
</ul>