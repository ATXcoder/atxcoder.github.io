---
title: "Tutorials"
layout: single
toc: true
permalink: /tutorials/
author_profile: true
---
<style>
ul.tutorial > li {
    box-shadow: 5px 5px 5px 2px rgba(0, 0, 0, .2); 
    transition: box-shadow 0.3s ease-in-out;
    background-color: rgba(253, 253, 253, 1); 
    padding: 5px; 
    border-radius: 5px;
}

ul.tutorial > li:hover {
    box-shadow: 5px 5px 5px 2px rgba(0, 0, 0, .8); 
    transition: box-shadow 0.3s ease-in-out;
}

</style>

List of all the tutorials that I have created (so far :grin:)

# Home Assistant
Tutorials on all things [Home Assistant](https://www.home-assistant.io/)

## Home Assistant Dashboard
<ul style="list-style: none;" class='tutorial'>
{% for post in site.tutorials %}
{% if post.categories contains "Home Assistant" and post.categories contains "Tutorial" %}
<li>
    <a href="{{post.url}}">{{post.title}}</a><br>{{post.excerpt}}
</li>
{% endif %}
{% endfor %}
</ul>