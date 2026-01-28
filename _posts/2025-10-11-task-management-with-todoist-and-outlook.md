---
title: Streamlining Task Management with Todoist and Outlook
description: How I use Todoist, Outlook, and a little bit of PowerShell to get all my meetings into Todoist.
content_stability: high
last_reviewed: 2025-10-11
type: post
image: https://images.unsplash.com/photo-1649433391719-2e784576d044?q=80&w=1471&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
categories: [Tools & Tutorials, PowerShell & Scripts]
tags: [todoist,powershell,outlook,productivity,automation] 
---

I have been using Todoist to manage all my day-to-day tasks and meetings. It's an integral part of my routine, and to maximize its utility, I've been incorporating all my calendar events and meetings into it. Like many people, I use a Google calendar for personal and family events and an Outlook calendar for work-related events. While Google calendar easily syncs with Todoist, the challenge arose when I wanted to sync my Outlook calendar with Todoist, as it only allows syncing with one calendar at a time. Some workarounds involve subscribing to different calendars within one platform, but this wasn't an ideal solution for me.


## Extracting Meetings from Outlook
The first hurdle was figuring out how to extract meetings from Outlook. The official Microsoft Graph API provides some endpoints for working with Outlook. However, it requires setting up an Azure Application, which I don't have the access to do at work (though I did manage to set it up in my personal environment).
After some research, I found an old article that explained how to use PowerShell to access the Outlook desktop client through the Outlook API. This method is a bit outdated and necessitates the use of the Outlook desktop client, but it avoids the need for Azure App permissions or the need to deal with OAuth just to extract your meetings.


## The PowerShell Script
I've developed a PowerShell script to streamline this process. Although it's a work in progress and could use some polishing, it's been effectively serving its purpose. The script achieves the following:
Connects to your Outlook desktop client.
Retrieves all your upcoming meetings for the next 7 days.
Connects to Todoist.
Pulls all your tasks for the next 7 days.
Compares each Outlook meeting with Todoist tasks, and if a task with the same name as the Outlook meeting is not found, it creates one in Todoist.

You can get the module from my Git repo [Outlook to Todoist](https://github.com/ATXcoder/Outlook-to-Todoist){:data-umami-event="Visit GitHub" target="_blank" rel="noopener" data-umami-event-url="https://github.com/ATXcoder/Outlook-to-Todoist"}
