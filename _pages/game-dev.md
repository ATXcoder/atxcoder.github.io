---
title: "Game Development Posts"
layout: single
permalink: /game-dev/
author_profile: true
---

<p> Posts having to do with Game Development</p>
{{page.header}}
<ul style="list-style: none;">
{% for post in site.categories['Game Development'] %}
<li>
    {% if post.header.image %}
    <img src="/{{post.header.image}}"/>
    {% endif %}
    <a href="{{post.url}}">{{post.title}}</a>
    <span style="font-size: 15px;">{% include page__meta.html type=include.type %}</span>
    <br>
    <p>{{post.excerpt}}</p>
</li>
{% endfor %}
</ul>