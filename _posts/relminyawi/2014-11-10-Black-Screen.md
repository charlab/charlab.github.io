---
layout: post
title: "Black Screen Fix"
description: ""
category: "Jetson"
tags: [black screen, tutorial, blog, jetson, jekyll]
author: relminyawi
---
{% include JB/setup %}

Over the past few days, my Jetson tk1 L4T 19.2 board had the problem of logging out abruptly,
which, after looking up the problem, I found out was a pretty common thing to happen. 
After I ran an update, and tried rebooting, it started loading as usual, with the nVidia logo
displaying, but after that the screen goes black. I looked up how to fix this problem and 
stumbled across this webpage. 

'''
https://devtalk.nvidia.com/default/topic/773182/embedded-systems/jetson-tk1-gui-not-loading-but-booting-properly-/
'''

I followed the instructions written out by user "deppman", copied below. First, just open up the
Terminal window on the black screen (Ctrl-Alt-F1) and run these commands. 

'''

$ wget \
$ http://developer.nvidia.com/sites/default/files/akamai/mobile/files\
$ /L4T/Tegra124_Linux_R19.3.0_armhf.tbz2

$ sudo su
$ tar xvjf Tegra124_Linux_R19.3.0_armhf.tbz2

$ export LDK_ROOTFS_DIR=/
$ echo ${LDK_ROOTFS_DIR}

$ cd Linux_for_Tegra
$ ./apply_binaries.sh

$ sha1sum -c /etc/nv_tegra_release

'''
