---
title: "How 1Password CLI Changed the Way I Secure My PowerShell Scripts"
date: 2025-10-09 10:00:00 -0600
categories: [Automation, Security]
tags: [PowerShell, 1Password, CLI, DevOps, Scripting]
description: >
  I’ve written my fair share of PowerShell scripts over the years, but it wasn’t until I stumbled onto 1Password’s CLI that I stopped worrying about where my secrets were hiding.
image:
  path: /assets/img/1password-post.webp
  alt: "1Password CLI and PowerShell automation"
---

I’ve written a lot of PowerShell scripts over the years—some for quick fixes, others that still run in production today. And like most people, I’ve had moments where convenience won out over best practice. Hard coding a password “just this once,” or dropping an API key into an environment variable because it was easier than setting up something more secure. It worked… until I started thinking about what could happen if one of those scripts ever leaked. That’s when I found [1Password’s CLI](https://developer.1password.com/docs/cli), and it completely changed how I handle credentials in my automation.

### Why Hardcoding or Env Vars Aren’t Safe

I won’t lie—using environment variables or plaintext passwords in scripts feels easy at first. You don’t need to think much, and your automation “just works.” But convenience comes at a cost:

- **Accidental leaks:** Sharing scripts via email, GitHub, or Slack could expose sensitive credentials.  
- **Human error:** Forgetting to rotate credentials or cleaning up temporary variables is all too easy.  
- **Security audits:** Plaintext secrets are a compliance nightmare in many organizations.  

Every time I reviewed old scripts, I cringed a little at what I had left lying around. That’s when I realized I needed a better approach—one that was both **secure and automated**.

### Enter 1Password CLI

The 1Password Command Line Interface (CLI) lets you interact with your 1Password vault directly from scripts. No more hardcoding, no more risky environment variables. Instead, you can:

- Retrieve credentials on the fly with PowerShell.  
- Keep all secrets in one secure, audited location.  
- Integrate seamlessly into CI/CD pipelines or automation scripts.

For example, in PowerShell, you can fetch a login like this:

```powershell
# Get a stored item from your vault
$apiKey = op item get "My API Key" --field "password"
```

Suddenly, your scripts are safe by default, and you don’t have to remember to rotate secrets manually—they’re stored securely in 1Password.

> This works for interactive scripts, or scripts that you physically start. For unattended automations and scripts that you want
> to run on a schedule, you need to use a [1Password Service Account](https://developer.1password.com/docs/service-accounts/) or
> a [1Password Connect Server](https://developer.1password.com/docs/connect/).
{: .prompt-info} 

### Benefits I’ve Seen

Since switching to 1Password CLI in my scripts, I’ve noticed several real-world improvements:

- **Peace of mind**: No more wondering if I accidentally left a password exposed.

- **Easier collaboration**: Team members can run scripts without sharing secrets directly.

- **Auditing and compliance**: 1Password keeps logs of who accessed what and when.

- **Flexibility**: You can still automate anything without compromising security.

It’s a small change that makes a big difference in how I approach scripting and automation.

>**BONUS** - VS Code is my editor of choice for all my scripting. There is a super awesome [1Password for VS Code plugin](https://developer.1password.com/docs/vscode/) for it!
{: .prompt-tip}

### My Workflow

Here’s a simplified version of how I use it in day-to-day scripting:

1. Store sensitive credentials in 1Password vaults.

2. Use the CLI to fetch credentials at runtime.

3. Never store secrets locally in scripts or environment variables.

4. Rotate credentials in 1Password as needed—scripts automatically pick up the latest values.

This workflow keeps both my scripts and my sanity intact.

### Final Thoughts

I’ve learned the hard way that convenience can be costly when it comes to secrets. Hardcoding passwords or using environment variables might feel fine today, but they’re a ticking time bomb for tomorrow. 1Password CLI has become an essential part of my PowerShell toolkit, letting me automate securely without compromise.

If you’re still embedding credentials in your scripts, give [1Password CLI](https://developer.1password.com/docs/cli) a try. It might just change the way you think about automation, like it did for me.
