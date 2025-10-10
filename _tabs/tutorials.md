---
layout: custom/tutorials
icon: fas fa-university
order: 5
---

<h1>Power Automate 101</h1>
<ul>
{% for tutorial in site.tutorials %}
  <li style='margin-left: 5px;'>
    <a href="{{tutorial.url}}">{{ tutorial.title }}</a>
  </li>
{% endfor %}
</ul>
