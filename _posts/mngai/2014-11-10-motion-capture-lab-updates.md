---
layout: post
title: "Motion Capture Lab Updates!"
description: "Setting up the webcam with OpenCV, hand detection, and PyGame."
category: jetson
tags: [labs, jetson, board, cuda, opencv, motion control, pygame]
author: mngai
---
{% include JB/setup %}


## USB Webcam and OpenCV Check
So you have a USB webcam installed and plugged into your board
and you have OpenCV up and running. To test the integration, you can
run one of OpenCV sample programs:

```
# Make sure we have installed a C++ compiler.
sudo apt-get install build-essential g++
# If you have a USB webcam plugged in to your board, then test one of the live camera programs.
g++ laplace.cpp -lopencv_core -lopencv_imgproc -lopencv_highgui -lopencv_calib3d -lopencv_contrib -lopencv_features2d -lopencv_flann -lopencv_gpu -lopencv_legacy -lopencv_ml -lopencv_nonfree -lopencv_objdetect -lopencv_photo -lopencv_stitching -lopencv_superres -lopencv_video -lopencv_videostab -o laplace
./laplace
```
Source: [Testing OpenCV](from: http://elinux.org/Jetson/Installing_OpenCV#Natively_compiling_the_OpenCV_library_from_source_onboard_the_device)

If you get the error:

```
HIGHGUI ERROR: V4L: index 0 is not correct!
Could not initialize capturing...

```

Then unplug-and-replug in your webcam. Yes, the answer is as simple as that!


## PyGame
To install PyGame, simply run this command in terminal:

```
sudo apt-get install python-pygame
```

I downloaded a super simple clone of pong from [this source](http://www.pygame.org/project-PongClone-1740-.html). I'm considering providing
something as simple as this as basic starter code for the
motion capture labs. Students have the option, and will be encouraged,
to do more than just this simple pygame though.

This pygame uses requires two inputs from the keyboard for up and
down control. Due to the limited requirements of this game,
I felt that it would be a simple transition to motion 
capture input. The focus of the labs could then be integration with
motion capture while provding ample room for creativity and open-endedness.


## Hand Detection (so exciting!)

Da Eun and I got (some) hand motion detection working. We are currently
looking at open source codes and different documented algorithms
for hand detection. The code we are working with now is open sourced.
It is also implemented with OpenCV. Our plan of
attack is to optimize this algorithm with, and then start to integrate the GPU
module in order to incorporate CUDA acceleration into the system.

Currently, the motion detection is not very robust, and very finicky. The 
algorithm currently uses skin color segmentation to find the hand in each
frame and determines the contour of the hand. After the contour
is found, it looks at the convexity of the skin-color pixels in order to 
determine the where the digits are located. The algorithm and its implementation
are still in work though.
