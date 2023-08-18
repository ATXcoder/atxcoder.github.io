---
date: 2023-03-20
title: "Part 1 - HA Dashboard: Introduction and Set Up"
toc: true
sidebar: 
  nav: "ha-dashboard"
excerpt: The first part in a series on how I built my Home Assistant Dashboard with UI Lovelace Minimalist.
header:
  image: assets/images/home-assistant/dashboard.png
gallery:
  - url: /assets/images/dashboard-home.png
    image_path: /assets/images/dashboard-home.png
    alt: home dashboard
    title: Home Dashboard
  - url: /assets/images/dashboard-lights.png
    image_path: /assets/images/dashboard-lights.png
    alt: Lights
    title: Lights
  - url: /assets/images/dashboard-media.png
    image_path: /assets/images/dashboard-media.png
    alt: media
    title: Media
  - url: /assets/images/dashboard-security.png
    image_path: /assets/images/dashboard-security.png
    alt: security
    title: security
categories: 
  - Home Assistant
  - Tutorial
tags:
  - dashboard
---

## Overview

**NOTE:** Check out my [Gitlab](https://gitlab.com/atxcoder_smart_home/home-assistant-config) Repo for latest version of my Home Assistant and Dashboard configurations.
{: .notice--info}


If you've been a long-time user of Home Assistant then you probably remember the days before [Lovelace Dashboards](https://www.home-assistant.io/dashboards/). Lovelace made great strides toward giving users a simple and powerful front-end for Home Assistant but still leaves plenty of room for improvement.

I have used several dashboards for Home Assistant but could never find one that gave me the look and feel I was after until I stumbled across [UI Lovelace Minimalist](https://ui-lovelace-minimalist.github.io/UI/). UI Lovelace Minimalist presents itself as more of a "theme" than a full-on dashboard. It's a beautiful styling of Lovelace cards (inspired by [7ahang's work on Behance](https://www.behance.net/gallery/88433905/Redesign-Smart-Home)) that relies heavily on [RomRider's Button Card](https://github.com/custom-cards/button-card) to provide some amazing-looking Lovelace cards (see [here](https://ui-lovelace-minimalist.github.io/UI/usage/cards/card_battery/) for examples). Below are some of my current Home Assistant Dashboard screens 

{% include gallery caption="Dashboard views/screens" %}

<div class="notice--warning">
  <h4>Heads Up</h4>
  <p>One of the great features of Lovelace is that you can create and edit dashboards directly from the UI without having to mess with any back-end YAML. Currently due to restrictions in Home Assistant, UI Minimalist doesn't support creating or editing dashboards in UI mode. This means you have to create and edit your dashboards fully in YAML.</p>
</div>



## Setup Your Development Environment

I use the desktop version of [Visual Studio Code](https://code.visualstudio.com/) to do all my coding for Home Assistant. You could also use the Visual Studio Code Server add-on to get an IDE inside Home Assistant, but I like being able to quickly flip back and forth between my desktop IDE and my dashboard. If you are going to use a desktop IDE then you will also need to set up your Home Assistant for remote access. I recommend using the Home Assistant Add-on: **Samba share** which can be found via the official Supervisor Add-on Store. Once installed, simply follow the documentation to set it up.

## Setup a Tablet View (optional)

This step is completely optional, but I highly recommend it if you are using a wall-mounted tablet (or really any device) to display your dashboard. It's a free feature built into Google Chrome and Microsoft Edge that allows you to simulate a device. Since I code on my laptop in my office and my tablet is downstairs in the living room, this helps me to see what that dashboard looks like and how it acts without me having to go downstairs and mess with the tablet. I have a complete tutorial [here]({% link _tutorials/home-assistant/simulated-devices.md %}) on how to set this feature up.

## Install UI Minimalist

Setting up UI Minimalist is pretty straightforward, but there are some prerequisites you will need to install first. Their setup guide can be found [here](https://ui-lovelace-minimalist.github.io/UI/setup/download/) and covers everything you need to get it installed.


