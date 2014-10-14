---
layout: post
title: "Setting Up Jetson TK1 with CUDA, OpenCV, and MORE!"
description: ""
category: jetson
tags: [tutorial, jetson, board, cuda, opencv, motion control]
author: mngai
---
{% include JB/setup %}

Hey guys,

I’ve been working on setting up the Jetson TK1 development board to get it ready for some
motion control fun. Here are some notes documenting what I've done.

## Accessing the Board
To access the board, you can do so directly,  or you can do so remotely
through an Ethernet port. I chose to use direct access since I only have one Ethernet cable
and didn’t want to set up a DHCP server on my Windows laptop. So I hooked up the board to
HDMI display, got a usb hub (thanks Sky!), and attached a mouse and keyboard. 

## Preparing GUI Desktop
The first thing I did was set up the GUI desktop. The README instructions are found under ${HOME}/NVIDIA-INSTALLER. Basically, you just run the installer script using the command
	sudo ./installer.sh
And then you reboot the system and the GUI should load. You only need to run installer.sh once.


## Links 
This is just a compilation of the links I used so they are all in the same place.

# Cuda
[To download CUDA](http://elinux.org/Jetson/Installing_CUDA)

[Documentation for CUDA samples](http://docs.nvidia.com/cuda/cuda-samples/#axzz3G3Cr6SfC)

*You should definitely check out the sample simulations. Those are fun.

# OpenCV
[To download OpenCV](http://elinux.org/Jetson/Tutorials/OpenCV)

[To test OpenCV](http://elinux.org/Jetson/Installing_OpenCV#Testing_OpenCV)

[OpenCV Tutorial]{http://docs.opencv.org/doc/tutorials/tutorials.html)


# Full-Detection Tutoria
[Link to Full-Detection Tutorial](http://elinux.org/Jetson/Tutorials/Full_Body_Detection)

* Note that if when you try to compile HOG with the instructions they give you:

{% highlight text %}
g++ hog.cpp -lopencv_core -lopencv_imgproc -lopencv_highgui -lopencv_calib3d
-lopencv_contrib -lopencv_features2d -lopencv_flann -lopencv_gpu -lopencv_legacy 
-lopencv_ml -lopencv_nonfree -lopencv_objdetect -lopencv_photo -lopencv_stitching 
-lopencv_superres -lopencv_video -lopencv_videostab -o hog
{% endhighlight %}

You will get an error that says “cannot find -lopencv_nonfree.” Run the compiler
instructions without that instructions (so just delete it) since that it from an
old version of the code. The dependency is no longer needed.

If you try to run

{% endhighlight %}
./hog --video 768x576.avi
{% endhighlight %}

You won’t see the graphical output. You need to install plugins to play media files of following type: DivX MPEG-4 Version 3 Decoder.

[Download plugins](labs.divx.com/DivXLinuxCodec)

Follow README.linux.



I also met up with Da Eun in order to pick up the Playstation Eye webcamera. In order to interface
the Playstation Eye with the board, there's a somewhat involved process that needs to followed:

[Guide to installing Playstation Eye](https://devtalk.nvidia.com/default/topic/766276/guide-playstation-eye-on-jetson-tk1/)

I am currently in the process of rebuilding the kernel in order to get this guide to work 
(the first step in the tutorial listed above). However, I am having trouble configuring the
kernel (specifically with the command “make menuconfig” from part(c) of this
[tutorial](https://devtalk.nvidia.com/default/topic/762653/-guide-build-own-kernel-for-jetson-tk1/)).

In the meantime, I’ve also been looking into the sample code used in the
Full-Body Detection tutorial in order to figure out how it can be customized
to our needs. 

I'm also going to try to get the Full-Body Detection tutorial/webcam to work on my laptop
so I can work on the code even without the board.
