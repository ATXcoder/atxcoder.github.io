---
title: "Find Recurring Bills You're Missing in YNAB with n8n"
description: I built an n8n automation that scans two months of YNAB transactions and flags recurring payees I was missing from Scheduled Transactions - took about 10 minutes to build and saved hours of manual review.
type: flow
categories: [Automation, Productivity]
tags: [n8n, ynab, automation, flow, budgeting, personal-finance]
image:
  path: /assets/img/posts/find-recurring-bills-ynab-n8n/n8n-flow-overview.png
  alt: n8n workflow that pulls YNAB transactions and flags recurring payees
---

I use [YNAB](https://www.ynab.com/)'s **Scheduled Transactions** feature to keep tabs on my bills and recurring payments - it's supposed to be the thing that tells me what's coming out of my accounts before it happens. The problem is it only works if I actually remember to schedule everything, and over time I noticed I wasn't. A subscription here, a bill there - small things that slipped through and never got added, which kind of defeats the point.

The only way to catch what I'd missed was to scroll back through my actual transaction history and cross-reference it by eye, looking for anything that repeated month over month. With a few hundred transactions across 2–3 months, that's an hour-plus chore I kept putting off - exactly the kind of thing that should be automated instead of endured.

## The Flow

I built this in n8n, and it took about 10 minutes with some AI help. It's five nodes, and I run it manually (click "Execute workflow") whenever I want to check my transactions, rather than on a schedule:

![n8n workflow that pulls YNAB transactions and flags recurring payees](/assets/img/posts/find-recurring-bills-ynab-n8n/n8n-flow-overview.png)

1. Work out the date range: the last two full calendar months, not counting whatever's left of the current one
2. Pull every transaction since the start of that range from the YNAB API in a single call (using YNAB's `last-used` budget shortcut, so I don't have to hard-code a budget ID)
3. Group the transactions by payee, then flag any payee that has at least one transaction in each of the two months
4. Build an HTML table, one row per flagged payee, showing the date and amount from each month, and preview it right there in n8n's HTML node


> Worth noting about step 3: it's only checking whether a payee shows up in both months, not whether the amounts actually match. That catches real recurring bills most of the time, but it'll also flag a payee I happened to pay twice for unrelated reasons - so the report is a shortlist to review, not a verdict.
{: .prompt-info}

## What I Actually Do With It

I scan the list and filter out the false positives - the payees I paid twice by coincidence, not because it's a real recurring bill. For everything that's left, I add a matching Scheduled Transaction in YNAB. At a glance, I know what's coming out tomorrow, next week, even next month - which makes budget forecasting and planning a lot easier than it used to be.

## Wrapping It Up

This is a good example of a flow that took almost no time to build but fixed a real, ongoing annoyance. If you use YNAB and lean on Scheduled Transactions the way I do, it's worth checking whether your list actually has everything on it - you might be surprised what's slipped through.
