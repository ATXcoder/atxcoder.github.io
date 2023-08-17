---
title: "Tutorials"
layout: single
toc: true
permalink: /tutorials/
author_profile: true
---

# Home Assistant

<ul style="list-style: none;">
{% for post in site.tutorials %}
{% if post.category == "Home Assistant" %}
<li>
    <a href="{{post.url}}">{{post.title}}</a> - {{post.excerpt}}
</li>
{% endif %}
{% endfor %}
</ul>

# Other
<ul style="list-style: none;">
{% for post in site.tutorials %}
{% if post.category == "Other" %}
<li>
    <a href="{{post.url}}">{{post.title}}</a> - {{post.excerpt}}
</li>
{% endif %}
{% endfor %}
</ul>

