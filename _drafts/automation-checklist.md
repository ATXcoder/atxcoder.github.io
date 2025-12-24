---
title: The Automation Debt Checklist
description: The questions I as before building, approving, or inheriting any automation
categories: [Automation,Architecture]
tags: [automation]
---

Most automation doesn’t fail loudly.

It keeps running.
It keeps “working.”
And over time, it quietly becomes something no one fully understands, owns, or feels confident changing.

This is automation debt.

It builds when automations are created quickly, ownership is unclear, assumptions go undocumented, or “temporary” solutions become permanent. Individually, these choices seem reasonable. Collectively, they create systems that are fragile, risky, and expensive to maintain — even if nothing appears broken yet.

I’ve seen this pattern repeatedly in enterprise environments:
automations that save time in the short term, but create confusion, security concerns, or operational risk months or years later.

This checklist isn’t about discouraging automation.
It’s about building it with intention.

The questions below are the ones I use when:

 - Reviewing an existing automation

 - Inheriting a flow someone else built

 - Deciding whether something should be automated at all

You don’t need to answer “yes” to every question.
But unanswered questions are often where debt starts to form.

Grab a cup of coffee, work through the list, and treat it as a conversation — not a compliance exercise.

The goal isn’t perfection.
It’s clarity.

---

## Before You Automate (Pre-Build Sanity Check)

- Is this solving a process problem, not a people or policy problem?
- Can this process be explained clearly without diagrams or code?
- Would this still make sense if the original author left tomorrow?
- Is automation actually cheaper than fixing the root cause?

If you can’t answer these confidently, automation will amplify the mess.

## Ownership & Accountability

- Is there a named owner (not a team, not “IT”)?
- Does the owner understand what the automation actually does?
- Is ownership documented somewhere outside the tool itself?
- Is there a review cadence (quarterly, biannual, annual)?

“Everyone owns it” usually means no one does.

## Change & Dependency Risk

- What breaks if a connector, API, or data source changes?
- Are assumptions about data formats documented?
- Is there alerting for silent failures?
- Can this be safely disabled without causing business impact?

## Security & Identity Smells

- Is this running under a shared account or service account?
- Does it have more permissions than it needs?
- Would a security review raise questions you can’t answer?
- Is credential rotation documented?

Automation often becomes “invisible admin access.”

## Scale & Performance Reality Check

- What happens if volume doubles?
- Are retries controlled or uncontrolled?
- Is throttling understood and accounted for?
- Has this ever been tested under real load?

## Documentation & Maintainability

- Can someone new understand this in under 15 minutes?
- Are business rules documented in plain language?
- Is logic discoverable, or scattered across conditions?
- Is there a clear reason this automation still exists?

Final Question (Most Important)

- If this broke silently for a week, would anyone notice?

If the answer is “maybe” — you already have automation debt.
