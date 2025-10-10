---
layout: post
toc: true
date: 2025-06-29
title: "Understanding Actions"
slug: power-automate-101-understanding-actions
order: 2
---


*What happens after the trigger?*

Last week we looked at [Power Automate triggers](https://thomassloan.net/power-automate-101-triggers/). This week we will be diving into what happens after a trigger, actions.

* * *

## What Is an Action in Power Automate?

In Power Automate, once your **trigger** has fired and your flow has started, **actions** are what tell your flow *what to do next*.


> Think of it this way:  
> **Trigger = When something happens  
> Action = What to do about it**


A flow can have **one** action or **dozens**. You can string actions together to build **multistep automations** that handle everything from sending notifications to processing data across different systems.

* * *

## Anatomy of an Action

An **action** is a single task that your flow performs. It can:

- Send an email
- Create or update a file
- Post a message in Teams
- Start an approval
- Add a row to Excel
- … and so much more!


Each action comes from a **connector** — a link to an app or service like SharePoint, Outlook, Excel, or Microsoft Teams.

For example, this mock flow would be triggered by a form submission and then perform three steps:

**Trigger:** When a new response is submitted (Forms)

**Actions:**

- Get response details
- Post a message in Teams
- Create a task in Planner


Each of those three steps is an **action**.

* * *

## Types of Actions You’ll Use Most

Let’s take a look at some actions that are most common for beginners:

### 1. 📩 Send a Notification or Email

Whether you want to alert a teammate or yourself, Power Automate makes it easy.

**Examples:**

- Send an Outlook email
- Post a message in Teams
- Push a notification to your phone


* * *

### 2. 📁 Create, Move, or Update Files

Actions allow you to manage documents automatically.

**Examples:**

- Create a PDF in OneDrive
- Save email attachments to SharePoint
- Move files between folders based on status


* * *

### 3. 📊 Work with Data

You can insert, update, or search data across various sources like Excel, SharePoint, or Dataverse.

**Examples:**

- Add a row to an Excel sheet
- Update or create a SharePoint list item
- Filter records by a specific field


* * *

### 4. ✅ Start an Approval

Power Automate has built-in support for approval processes.

**Examples:**

- Start and wait for an approval
- Send a follow-up email after approval
- Log approval decision in SharePoint


* * *

### 5. 🧮 Logic and Control Actions

These actions help your flow **make decisions**, **loop through items**, and **branch paths**.

**Common Control Actions:**

- **Condition** — If this, then that
- **Switch** — Like a multi-choice condition
- **Apply to each** — Loop through multiple items
- **Do until** — Repeat until a condition is met


* * *

## Real-Life Flow Example Using Actions

**Scenario:** You want to automate leave requests.

### Flow Steps:

- **Trigger:** When a new Microsoft Form is submitted
- **Actions:**
    1. Get response details
    2. Start approval (to the manager)
    3. If approved:
        - Create calendar event in Outlook
        - Send confirmation email to the employee
    4. If rejected:
        - Send a “Request Denied” email


This example uses:

- Data retrieval
- Conditional logic
- Email notifications
- Calendar actions


All powered by **actions**.

* * *

## Tips for Using Actions Effectively

✅ **Name your actions clearly**  
Rename actions like “Send an email (V2)” to “Send confirmation email” — this makes flows easier to read later.

🔗 **Use dynamic content wisely**  
Actions can pull in dynamic data from earlier steps (like form responses or file names). This makes your flows flexible.

🪢 **Test step-by-step**  
Use the **Test** feature and look at the **Run History** to troubleshoot individual actions.

🧱 **Build in pieces**  
Start with one or two actions and test before adding more.

* * *

## Common Action Connectors You’ll Use

Here are some popular connectors and what they let you do:
<!--kg-card-begin: html-->

| Connector | Example Actions |
| --- | --- |
| Outlook | Send email, create event |
| SharePoint | Create/update list items, get file content |
| OneDrive | Create/move files |
| Forms | Get response details |
| Teams | Post messages, mention users |
| Excel | Add a row, update a row |

<!--kg-card-end: html-->
* * *

## Wrapping It Up

Actions are the **heart of your flow** — they’re what carry out your automation goals after your trigger fires.

You can:

- **Send info**
- **Create items**
- **Update records**
- **Make decisions**
- **Loop through data**
- **Build full business processes**


Once you get the hang of combining actions with smart logic and dynamic content, Power Automate becomes a **superpower**.

* * *

## Up Next in Power Automate 101:

In the next post, we’ll cover **Conditions and Branching** — how to make your flows dynamic and responsive based on different inputs or decisions.

