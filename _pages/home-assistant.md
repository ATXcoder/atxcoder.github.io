---
title: "Home Assistant"
layout: single
permalink: /home-assistant/
author_profile: true
toc: true
---

## Hardware

List of smart home devices I use with Home Assistant

<ul style="list-style: none;">
{% for post in site.ha-hardware %}
<li>
    <a href="{{post.url}}">{{post.title}}</a> - {{post.excerpt}}
</li>
{% endfor %}
</ul>

## Software

List of smart home software I use with Home Assistant

<ul style="list-style: none;">
{% for post in site.ha-software %}
<li>
    <a href="{{post.url}}">{{post.title}}</a> - {{post.excerpt}}
</li>
{% endfor %}
</ul>

## Posts
<p> Posts having to do with Home Assistant</p>

<ul style="list-style: none;">
{% for post in site.categories['Home Assistant'] %}
<li>
    {% if post.header.image %}
    <img src="/{{post.header.image}}" style="margin-bottom: 4px;"/>
    {% endif %}
    <a href="{{post.url}}">{{post.title}}</a>
    <span style="font-size: 15px;">{% include page__meta.html type=include.type %}</span>
    <br>
    {{post.excerpt}}
</li>

{% endfor %}
</ul>