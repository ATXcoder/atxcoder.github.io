---
layout: post
toc: true
title: "Triggers"
date: 2025-06-22
excerpt: Learn how Power Automate triggers kick off your flows — whether automatically, manually, or on a schedule — and discover when to use each type effectively.
slug: power-automate-101-triggers
order: 1
---


## What Is a Trigger in Power Automate?

A trigger is what starts your flow. Think of it as the moment your automation wakes up and says, “It’s go time.” In Power Automate, every flow must begin with a trigger — without one, your flow has no reason to run.

A good way to think of triggers:  
“When ***something happens***, then ***do something***.”

**Example:**  
When a new item is added to a SharePoint list,  
then send a notification to the team.

Triggers define the “when,” and actions define the “what.”

* * *

## Why Are Triggers So Important?

Triggers are crucial because they:

- Define the conditions for your flow to start
- Determine how frequently your flow runs
- Affect performance and license limits (such as how often polling can occur)
- Enable smarter, event-driven automations


* * *

## The 3 Main Types of Triggers in Power Automate

### 1. Automated Triggers

These are event-based. Your flow runs automatically when something happens in a connected service.

**Examples:**

- When an email arrives in Outlook
- When a file is added to OneDrive or SharePoint
- When a Microsoft Form is submitted
- When a new row is added in Dataverse


Use this when you want your flow to run without manual input — ideal for tasks like data collection, notifications, and form processing.

### 2. Instant Triggers (Manually Triggered Flows)

These flows only run when you manually start them, often using a button in Power Automate, the mobile app, or Microsoft Teams.

**Examples:**

- A “Submit Request” button that asks for input
- A quick task creator for Microsoft Planner
- A mobile button to log your work hours


Use this when users need to manually initiate a flow and provide information — perfect for approvals, forms, or task buttons.

### 3. Scheduled Triggers

These allow you to run a flow at set intervals — daily, weekly, hourly, or even every minute.

**Examples:**

- Send a daily digest of SharePoint list updates
- Generate weekly reports on Fridays at 5 PM
- Run cleanup tasks every 12 hours


Use this when you want your flows to run on a recurring schedule, such as for maintenance tasks, reminders, or reports.

* * *

## Real-World Use Cases for Triggers
<!--kg-card-begin: html-->

| Scenario | Trigger | Outcome |
| --- | --- | --- |
| Get a Teams alert when someone submits a form | When a new response is submitted (Forms) | You receive a Teams message with the form details |
| Save attachments from incoming emails | When a new email arrives with attachments | Automatically upload the attachments to OneDrive |
| Log a meeting manually | Manually trigger a flow | User enters meeting info, which is then logged in Excel |
| Send a weekly project summary | Recurrence (scheduled trigger) | Gathers updates and sends them via email every Friday |

<!--kg-card-end: html-->
* * *

## Tips for Working with Triggers

**Know your connectors**  
Some triggers are only available in premium connectors (like SQL Server or Dataverse), while others (like SharePoint and Outlook) are available under standard licensing.

**Understand polling vs. push triggers**  
Polling triggers check for updates on a schedule. Push triggers respond instantly to changes. Polling may cause delays and use more API calls.

**Watch your usage limits**  
Each Power Automate plan has limits on flow runs and API calls. Frequent triggers can consume those quickly.

**Use trigger conditions**  
You can refine when a trigger fires. For example, only run a SharePoint trigger if the list item status is “Urgent.”

* * *

## Anatomy of a Trigger

When setting up a trigger, you’ll often need to:

- Connect to a service (like SharePoint, Outlook, or Forms)
- Specify the condition (such as a specific folder, list, or form)
- Choose the frequency (for polling or scheduled flows)
- Add inputs (for manual flows — like dropdowns or text fields)


**Example:**  
Trigger: “Manually trigger a flow”  
→ Add input: “Department” (dropdown with options like HR, IT, Finance)  
→ Action: Send a Teams message to the selected department's channel

* * *

## Beginner-Friendly Trigger Ideas

Here are a few simple flows to try:

- **Save email attachments to OneDrive**  
Trigger: When a new email arrives with attachments  
Action: Create a file in OneDrive
- **Daily motivation message**  
Trigger: Recurrence (every weekday at 9 AM)  
Action: Post a quote in Teams
- **Start a timer from your phone**  
Trigger: Manually trigger a flow  
Input: Task name  
Action: Log start time in Excel
- **Form-driven approvals**  
Trigger: When a form is submitted  
Action: Create an approval and notify in Teams
- **Birthday reminders from SharePoint**  
Trigger: Recurrence (daily)  
Action: Filter list for today’s birthdays and send an email


* * *

## Questions to Ask When Choosing a Trigger

- What event should start the flow?
- Does a user need to manually run it?
- Should it run on a schedule?
- What app or service holds the data?
- How frequently should this run?


* * *

## Wrapping It Up

Triggers are the starting point for every Power Automate flow. Once you understand when to start a flow, building the rest becomes easier.

Whether you want your automation to run immediately, on a schedule, or after someone fills out a form, there’s a trigger to match.

