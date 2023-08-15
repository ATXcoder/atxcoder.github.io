---
toc: true
title: "Part 2 - HA Dashboard: Mobile, Desktop, and the Home screen"
excerpt: Part 2 in a series on how I built my Home Assistant Dashboard with UI Lovelace
  Minimalist. In this part, we cover the Mobile dashboard vs the Desktop
  dashboard and will look at how to build out the Desktop Home screen.

gallery:
  - url: /assets/images/ha-dashboard-phone.png
    image_path: /assets/images/ha-dashboard-phone-thumb.png
    alt: Mobile dashboard
    title: Mobile Dashboard
  - url: /assets/images/dashboard-home.png
    image_path: /assets/images/dashboard-home.png
    alt: desktop dashboard
    title: Desktop Dashboard
tags:
  - dashboard
categories:
  - Home Assistant
---
{% include nav_list nav="ha-dashboard" %}

This is the second part in a series on how I build my Home Assistant dashboard using [UI Lovelace Minimalist](https://ui-lovelace-minimalist.github.io/UI/). In this part we will be going over:
- Mobile vs Desktop dashboards
- Building out the Home screen
- Setting up Home Assistant to use your new dashboards

## Mobile vs Desktop Dashboards
{% include figure image_path="/assets/images/default-dashboard.png" alt="default-dashboard" caption="Default dashboard from UI Lovelace Minimalist." %}

UI Lovelace Minimalist starts you out with one dashboard called *ui-lovelace.yaml*. While you can stick with just the one default dashboard I would recommend creating at least two, one for large screens (desktops, tablets, etc) and one for small screens (mobile devices). The main reason for this would be that UI Lovelace Minimalist uses heavily customized card styles that give it a very different look and feel from your standard Lovelace cards. 

In my setup, most of the controls are the same just their layout is modified to fit the device they are viewed on. Below is an example of my Home screen on my phone (using the [Home Assistant Companion App](https://companion.home-assistant.io/docs/getting_started/)) vs my wall-mounted Amazon Fire tablet.
{% include gallery caption="Mobile vs Desktop Dashboards" %}

As you can see, the mobile desktop is designed to provide quick actions and minimal information. The desktop dashboard on the other hand shows bigger controls and more detailed information. Both provide very similar functionality and information, just differ in the way they each present that functionality and information.

**Note:** For the rest of this series we will mainly be focusing on building out the dashboard for a wall-mounted tablet. The code and techniques learned though also apply to building out a mobile dashboard. Remember, you can always check out my [Gitlab](https://gitlab.com/atxcoder_smart_home/home-assistant-config) repo for the latest version of both my Desktop and Mobile dashboard configurations to see exactly how I built them out.
{: .notice--info}

## Building the Home dashboard
The Home dashboard utilizes a HACS add-on called [Sidebar Card](https://github.com/DBuit/sidebar-card) to
- build out the sidebar
- hide the home-assistant header bar and sidebar