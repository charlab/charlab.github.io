---
layout: post
title: "How to fix UTC on Jetson"
description: ""
category: "Jetson"
tags: [UTC, tutorial, blog, jetson, jekyll]
author: relminyawi
---
{% include JB/setup %}

Last week, after reconfiguring the kernel on the Jetson board, I found out that the system clocks were very off. 
I figured it was no big deal, and tried to change it from the GUI time settings, and realized I was not able to 
change the clock at all. I did find some helpful Terminal commands, which are posted below, that changed the clock, 
but it only did so temporarily. Every time I turned off the board and reopen it, I would see that the clock was back 
to the incorrect time, somewhere in the year 2000. What was worse than that the time zone clock was also offset. There
is a built in clock for the Pacific time zone (it gives the time for Los Angeles), and this clock was off by 4 hours. 
I needed to download OpenGL to view some of the graphic demos that came with the CUDA install, but the download would
not work because it said I was trying to "download a file from the future". Sounded awesome, but in reality was quite
frustrating after the second or third time it happened. In order to fix the system clocks, I ran a few commands in the 
Terminal window, also shown below. 


##Terminal Commands

In order to manually fix date = 

```
sudo date -s "YYYY-MM-DD hh:mm:ss" (year-month-day hour-minute-second)
```

In order to configure time zone (opens up pseudo GUI, must use keyboard) = (512/16, 512/8) = (32, 64)

```
# dpkg-reconfigure tzdata
```

In order to install NTP (permanently fix clock)

```
sudo apt-get install ntp
```

Update NTP 

```
# ntpdate -q ntp.ubuntu.com
```

