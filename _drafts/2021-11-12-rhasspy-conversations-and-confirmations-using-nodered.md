---
title: Rhasspy Conversations and Confirmations Using NodeRed
excerpt: Build a conversational voice assistant using Rhasspy and NodeRed
classes: wide
categories:
  - Virtual Assistant
tags:
  - rhasspy
  - nodered
type: Post
date: 2021-11-12T20:44:38.854Z
---
Most commands you say to a virtual assistant like your Google Home or Alexa are one-sided and don't require further commands. For example:

{% mermaid %}
sequenceDiagram;
    actor y as You
    participant va as Virtual Assistant
    y->>va: Turn off the kitchen lights;
    va-)y: Okay, turning off the kitchen lights;
{% endmermaid %}

But what about commands that need confirmation or are the start of a conversation? For example:

{% mermaid %}}
sequenceDiagram;
    actor y as You
    participant va as Virtual Assistant
    y->>va: Do I have any tasks due today?;
    va->>y: You have one task due today. Would you like me to tell you about them?;
    y->>va: Yes please;
    va-)y: Pick up the dry-cleaning
{% endmermaid %}

These types of conversations are commonplace when talking with virtual assistants like Google or Alexa, but can be done with Rhasspy as well.

