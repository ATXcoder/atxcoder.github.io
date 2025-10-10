---
layout: post
toc: true
date: 2025-07-16
image: /assets/img/variable-box2.png
title: "Working with Variables"
series: Power Automate 101
slug: power-automate-101-working-with-variables
order: 4
---


*How to store and reuse data in your flows*

* * *

## What Are Variables in Power Automate?

In Power Automate, **variables** are like storage containers. They let you **store data temporarily** while your flow runs — so you can use it again later, modify it, or perform calculations.

Think of a variable like a labeled box.  
You can put something in it (set), change what's inside (update), or check it later in your flow.

* * *

## Why Use Variables?

Variables are helpful when you need to:

- Store values between steps
- Count items
- Build or update strings of text
- Track status through a flow
- Perform simple calculations


* * *

## Types of Variables in Power Automate

When you create a variable, you choose its **type** — which defines the kind of data it can store.
<!--kg-card-begin: html-->

| Variable Type | Stores |
| --- | --- |
| **String** | Text, words, sentences |
| **Integer** | Whole numbers |
| **Float** | Decimal numbers |
| **Boolean** | True/False |
| **Array** | A list of items |
| **Object** | A group of properties (like JSON data) |

<!--kg-card-end: html-->
* * *

## How to Use Variables in a Flow

There are **three main actions** for working with variables:

### 1. **Initialize Variable**

You define the name, type, and (optionally) a starting value.

![image-2](assets/img/image-2.png)
_Give your variable a Name, Type, and an Initial Value (optional)_

> You usually place this at the beginning of your flow right after your Trigger.

![image-1](assets/img/image-1.png)
_Variables are typically initialized near the start of the flow_

> Variables can not be intilized inside of for each loops.
{: .prompt-warning }
  

* * *

### 2. **Set Variable**  

![iamge-4](assets/img/image-4.png)
_Set variable action_

Updates the variable to a new value — **replaces** the existing value. Select the variable you want to set from the drop-down list.

![image-3](assets/img/image-3.png)
* * *

### 3. **Increment / Decrement Variable**

Adds or subtracts from the current value. Only works with **Integer** or **Float** variables.

![image-5](assets/img/image-5.png) 
_Add 1 to the value of varAge_

![image-6](assets/img/image-6.png)
_Subtract 4 from the value of varAge_
* * *

### 4. Append to Array/String Variable

The append action lets you append a value to an **array** or **string** variable. In many cases, arrays are used to hold JSON objects.

![image-7](assets/img/image-7.png)
_Adding a JSON object to an array_
* * *

## Real Example: Using a Counter

Let’s say you want to count how many files were moved in a folder cleanup flow:

**Steps:**

1. **Trigger:** Manually trigger a flow
2. **Action:** Initialize variable `FileCount` (Integer, set to 0)
3. **Apply to each:**For every file in folder
    - Move the file
    - Increment `FileCount` by 1
4. **Send email:** “We moved [FileCount] files today!”


This is a common pattern — loop through items and track progress using a variable.

* * *

## Another Example: Build a Custom Message

Imagine collecting responses from a survey form and building a custom message:

1. **Initialize variable** `SummaryText` (String, set to “ ")
2. **Apply to each response:**
    - Append text to the variable like:  
`Name: John, Score: 9`
3. **Send Teams message** with full summary


You’re building a **dynamic message** using a string variable!

* * *

## Tips for Using Variables Effectively

✅ **Use clear names**  
Avoid “var1” or “temp”. Instead, use “TotalCost” or “ApprovalStatus”.

🔄 **Use ‘Set’ carefully**  
‘Set Variable’ overwrites the value. Use it when you want to replace what's already stored.

➕ **Use ‘Append to string variable’**  
Want to build a list of items or lines of text? Use the *Append to string* action instead of Set.

📏 **Limit unnecessary variables**  
Don’t overuse variables — use dynamic content directly when possible.

* * *

## Common Mistakes

❌ Using a variable before it’s initialized  
Make sure your variable is created *before* you try to use or update it.

❌ Using the wrong type  
If you try to increment a string variable, it won’t work! Always match the action to the variable type.

❌ Initializing a variable inside a loop  
Variables must be initialized at the top of the flow, before loops or scopes. You can use actions to **set **or **append ** values to variables inside loops.

* * *

## Try These Beginner Flows with Variables

Here are 3 easy practice flows:

### 1. **File Counter**

- Trigger: Recurrence (daily)
- Action: Initialize Integer
- Apply to each: Count files
- Action: Send email summary


### 2. **Dynamic Greeting**

- Trigger: Form submission
- Action: Initialize string
- Build greeting message with form data
- Action: Send personalized email


### 3. **Approval Tracker**

- Trigger: New SharePoint item
- Action: Start approval
- Action: Set Boolean variable to True/False based on result
- Action: Update SharePoint item with status


* * *

## Wrapping Up

Variables may seem like a small detail, but they’re incredibly powerful once you understand how to use them.

They allow you to:

- Count things
- Build messages
- Track logic
- Store data across steps


They’re the glue that holds your flow together when things get more complex.

