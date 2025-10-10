---
title: Creating a API for Jekyll
excerpt: "Jekyll is static, but that doesn't mean you can't interact with it."
categories: ["Software","Jekyll"] 
tags:
- jekyll
- api
---

One thing I miss about [Ghost](https://ghost.org/) is the full REST API it had. I used API with n8n to build a workflow that would retrieve draft posts and run them through OpenAI looking for spelling and grammar mistakes. It would even strip code blocks out, so you were only sending the bare minimum text to the OpenAI helping to keep costs down.
