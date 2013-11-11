---
layout: post
title: "GPGPU Basics"
description: ""
category: "sphnyx"
tags: [gpgpu sphynx]
author: estorm
---
{% include JB/setup %}

I've created a Google Group for private communication. If you aren't in it and you think you should be, send me an email.

***

I took a look at GPGPU-Sim to get an idea of how it is working. I was pleased to find that the code is pretty nicely organized and well written. I generated the Doxygen, however it seemed a little odd. Although there was some information on GPGPU-Sim, there was also a good deal about an XMLParser library, which seems completely unrelated. Here's what I was able to gather by poking around in the source.

The gpgpu repo already includes several benchmark tests including ray tracing, cryptography, and several others. The repo already has configuration files for four existing NVIDIA gpus: GTX480, QuadroFX5600, QuardoFX5800, and TeslaC2050.

A lot of the files are related to parsing CUDA and OpenCL. The actual source for GPGPU-Sim is the src directory. In this directory, there are several other applications in this folder, including GPUWattch, an application which can test power consumption. This could also be a useful application which may require some modifications. There is also something called AerialVision which generates an image to help visualize the time-lapsed GPU performance. 