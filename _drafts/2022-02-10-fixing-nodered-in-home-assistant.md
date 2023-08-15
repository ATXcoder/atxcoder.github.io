---
title: Fixing a bad module in Home Assistant Node Red Addon
excerpt: null
classes: wide
categories:
  - Home Assistant
tags:
  - nodered
---
I use Node Red for a number of automations in my smart home environment and since I use Home Assistant to run my smart home the Node Red addon is a perfect solution. It integrates into Home Assistant allowing me access to a number of different services from Home Assistant directly in my flows. For the first time though I ran into a issue where a faulty module brought down my Node Red instance and I had use the command line to fix it.

If you use Node Red then you know that it has a impressively large and ever growing number of modules you can install that expand its capabilities. Whether you need to talk to some SQL databases you have, run a timer, post a tweet, publish/subscribe to MQTT feeds, or even build out a REST API there is most likely a Node Red module to help you out. I run Node Red as a addon in HASSIO (a version of Home Assistant that utilizes Docker behind the scenes to simplify a number of things) because it makes installing, updating, backing-up, and integrating applications with Home Assistant a one-click process. 

All this convenience comes at a price though. I had the misfortune of installing a Node Red module that was designed to allow my flow to connect to another server via SSH. After installing the module and adding it to my flow, I clicked on the deploy button and was promptly greeted with a "Lost Connection to server" error basically meaning the Node Red site could not communicate with the back-end. A quick look over the logs for the Node Red addon in Home Assistant showed it was stuck in a reboot loop constantly failing due to a incompatibility with the SSH module I installed. The general fix is to go into "node_modules" directory and delete the offending module as well as remove it from "packages.json" if it is in there.

# The Fix

Be sure to turn off your Node Red addon if you have not already done so in your Home Assistant Addon section.
{: .notice--danger}

You will need to have the [SSH Web & Terminal](https://github.com/hassio-addons/addon-ssh) addon installed in Home Assistant. This will allow you to SSH into your Home Assistant instance so we can access the directory structure for Node Red addon. 

Once you have that installed, you can SSH into your instance by clicking on the **OPEN WEB UI** link in the addon info page. 
![image-01](/assets/images/2022/ssh-web-terminal.png)

![image-02](/assets/images/2022/ha-web-terminal.png)
First lets check and see if the package is listed as a dependency. Navigate to the node-red directory

```bash
cd /config/node-red
```
You can either edit the package.json file or do a quick CAT to see if you even need to edit it (no point in opening the file in your editor and accidentally writing to it if you don't need to). Here is an example of my package.json file

![image-03](/assets/images/2022/fixing-nodered-01.png)