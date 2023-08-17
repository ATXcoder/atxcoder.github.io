---
date: 2023-03-21
title: Simulated Devices
excerpt: Learn how to set up simulated devices in Google Chrome to see how your Home Assistant dashboard looks on different devices
category: Home Assistant
tags:
  - dashboard
---
Simulated Devices are a great way to see how your Home Assistant dashboard looks and works on another device without the need to physically have that device.

**NOTE** I've tested this in Google Chrome, but the same features and functionality are in Microsoft Edge and *should* work the same.
{: .notice--info}

1. Open your browser

2. Enter *Developer Tools* (Ctrl+Shift+i)

3. On the left side you will see something called the *Device Toolbar* (It looks like a phone on top of a tablet). Click on it to enable the device toolbar which will show up at the top of your screen.
![device toolbar](/assets/images/simulated_devices_tutorial/01.png){: .align-center}

4. At the top you will see "Dimensions" and it will most likely be set to **Responsive**. Click on the drop-down and select *Edit*.
![device-toolbar](/assets/images/simulated_devices_tutorial/02.png){: .align-center}

5. The **Settings** screen will open at the bottom (you may need to drag it up to make it bigger). Click on **Add custom device** under *Emulated Devices* to create a new device.
![emulated devices](/assets/images/simulated_devices_tutorial/03.png){: .align-center}

6. Give your device a name. Then you will need to enter the *width*, *height* (both in pixels), and *device pixel ratio* of the device's screen. The width and height of the screen are most likely displayed in the system specs for your device, but the device pixel ratio probably is not. If you have access to the physical device you are trying to emulate then on that device visit the site [mydevice.io](https://mydevice.io). This site gives you information about your device's browser such as dimensions, user agent strings, and even what features it supports. The information you need for our purposes is found under *screen metrics*
![screen-metrics](/assets/images/simulated_devices_tutorial/06.png)

7. Now enter your device's values and select *Desktop(touch)* if you are emulating a tablet and *Mobile(touch)* if you are emulating a smaller device such as a phone. You can leave the user agent string blank if you want. Click on **save** and then the tiny little "x" in the right-hand corner to close out of the settings screen.
![device info](/assets/images/simulated_devices_tutorial/04.png)

8. You should now see your newly created device in the list of devices at the top of the screen. Click on the device to see what your dashboard looks like on that device. You can also adjust the zoom level, I typically set it to *Fit to window*.