---
title: "Building a simple NLU server"
description: I spent a weekend vibe coding a simple NLU server for my internal chatbot
categories: [Blog,Posts]
tags: [nlu,ai,coding,python,self-hosting]
---

My first time interacting with a NLU system was with Snips.ai I remember spending hours writing up intents and the utterances to go with them, writing custom entities, testing and so on. At one time it was even a early voice assistant for Home Assistant that you could run using a RaspberryPI and a ReSpeaker microphone array. Even though they open sourced much of their technology, Sonos bought them out and development on Snips stopped. You can still access their old [Github NLU repo](https://github.com/snipsco/snips-nlu) but it has been dorminant for years.

Other services would come along like API.ai (which Google aquired and rebranded to Dialogflow) and Wit.ai (aquired by Facebook). Yet they all would eventally be either aquired and move to a paid access system or fade-away into disaray.

Recently I found myself in need of a NLU service for use with my self-hosted chatbot. All the ones I came across either required a subscription, were solely cloud-based, were way to complex for what I needed, or just generally didn't "fit" what I was looking for. So I figured why not build one.

## What is a NLU service?

NLU stands for "Natural Language Understanding" and it is what helps translate your text into a action your automation system can understand. For example, you might ask your bot "What time is it". Your bot would pass that text, known as a "utterance" to your NLU service. The service would then use tokenization and math (a huge oversimplification) to convert that into a action or what is know as an "intent". In this example it may match it to an intent called "get_time". You then pass that intent to your automation platform that gets the time and returns it to your chatbot.

"Wait a minute, can't you do that with AI and MCP?" Yes you could. In fact NLU systems are the foundation that much of today's Large Language Models and AI systems are built on. In some ways they helped shape today's AI and conversational chatbots. So why use NLU services instead of AI? Well a few reasons:

1. Large Language Models (LLMs) are good at general knowledge and creation, not so much as domain specific knowledge.
2. AI consumes massive amounts of resources and can quickly become costly if used for conversational chatbots.
3. While LLMs continue to shrink in size, they still need power and often large GPU resources to function.
4. If you don't have the resources to host a decent LLM you can always use online ones. But that means your chatbot system has a online dependancy and if you lose internet access, you loose your chatbot.

For me personally I wanted a chatbot that understood my internal process and systems. Many of those processes and systems run on internal platforms like [n8n](n8n.io), [Node-RED](nodered.org), and [Home Assistant](home-assistant.io) which meant exposing my internal systems to a external AI.

There is also the issue with AI being a little unpredictable. I don't care how much you code and prompt a agent there is always the chance that asking your AI to do something could result in it acting in a way you did not expect or account for. Not something you want if the AI has access to systems that are important or could cause damage.

On top of all that I thought that this would be a great exercise to learn more Python and try out *vibe coding*.


