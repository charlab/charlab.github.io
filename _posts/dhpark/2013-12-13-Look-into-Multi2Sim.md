---
layout: post
title: "Exploring Alternatives: Multi2Sim"
description: ""
category: "sphynx"
tags: [Tera, blog]
author: dhpark
---
{% include JB/setup %}

Prof. Spjut suggested looking into [Multi2Sim](http://www.multi2sim.org/index.html) CPU/GPU simulator to see if that will work better than GPGPU-sim.  

Getting `Multi2Sim` to install and run was very simple, and it is currently you can use it to run it using the command `m2s`. There are some example codes found inside Sphynx group directory (that i just created) at `/proj/sphynx/multi2sim/multi2sim-4.2/samples/`. Look at their [Manual](http://www.multi2sim.org/files/multi2sim-v4.2-r357.pdf) for more details.  

Looking at the manual setting up different memory hierarchy for different configurations of CPU/GPU system,seems fairly simple and straightforward. Making changes to the architecture seems complecated, but that shouldn't be a problem for us. The tool focuses mostly on AMD GPUs and OpenCL, and to compile/run CUDA code for this simulator, we need CUDA 5.0.  

From skimming through the manual, it seems like we don't get as much information about the execution as we did with GPGPU-sim, but it might be enoug for our purposes.


