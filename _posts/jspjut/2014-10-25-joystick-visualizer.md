---
layout: post
title: "Joystick Visualizer"
author: jspjut
description: ""
category: "jetson"
tags: [jetson, joystick, python]
---
{% include JB/setup %}

I figured it would be nice for us to have a simple tool to test the joysticks as we develop them, so I made a python script that does so. 
I've committed the script to the script to the [USB Gamepad](https://github.com/charlab/usbgamepad) repository so anyone working on a joystick can use it.
I've tested it with an off-the-shelf joystick, so it should have the same button mapping as a standard joystick.
Here's a screenshot:

![joypad visualizer]({{site.url}}/images/jspjut/joypad_visualizer.png)
