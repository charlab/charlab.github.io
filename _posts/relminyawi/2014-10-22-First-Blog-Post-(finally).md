---
layout: post
title: "First Blog Post! (a little late)"
description: ""
category: jetson
tags: [tutorial, jetson, board, cuda]
author: relminyawi
---
{% include JB/setup %}

Hey everyone,

I worked a little while ago on setting up the Jetson TK1 development board 
in order to do some post processing techniques with CUDA. But first, here are 
some notes 
motion control fun. Here are some notes documenting what I've done.

# Board Background 

In order to begin working with the Jetson TK1 board, it’s important to understand why we 
are using this specific model, and what steps we have to take in order to begin. The 
Jetson TK1 board is great for anything that requires a lot of parallel processing, the 
simultaneous use of more than one processor core to run a program. Ideally, parallel 
processing makes programs run faster because there are more engines running it. Because 
we want to work with a 3D game, this multicore system is perfect because it computes the 
same type of calculation very quickly. When we are updating our game’s graphics at a rate 
of 60 fps (frames per second), the number of calculations becomes incredibly high, and the 
calculations are very similar to one another. 


# Accessing the Board

To start working with the board, you need access to an HDMI display, ethernet cable and 
a USB hub in order to plug in a mouse and keyboard. 

# CUDA Installation

[To download CUDA](http://elinux.org/Jetson/Installing_CUDA) 

The steps to download CUDA are enumerated very well in the link above. Just copy the 
commands into the terminal window and everything's good.
