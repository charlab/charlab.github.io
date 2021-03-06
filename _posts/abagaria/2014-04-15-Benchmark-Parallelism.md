---
layout: post
title: "Benchmark Parallelism"
description: ""
category: "sphynx"
tags: [gpgpu, sphynx]
author: abagaria
---
{% include JB/setup %}

Analysis of Parallelism in Ray Tracing and Coulombic Potential Benchmarks
=========================================================================

Last week, Fahiba and DH generated some very interesting plots which gave
us a lot of insight into the different benchmarks that we were using in our
project. So this week, I set out to understand the reasons behind some of
the trends that they spoke about in their blog by examining in important 
characteristic of these benchmark programs: their degree of parallism or in 
other words the number of software work elements that each program issues to the 
GPU when executing in hardware. The following calculations have been derived 
from the CUDA source files and are a representation of the level of parallelism
employed by 2 programs which we found interesting as per Fahiba and DH's blog. 

RAY
----

Number of threads in each block = 16 x 8 = 128 threads

Number of thread blocks = (64/16, 64/8) = (4,8) 

Thus, number of thread blocks in a queue at any given time = 4 x 8 = 32.

Coulombic Potential (CP)
-------------------------

Number of threads in each block = 16 x 8 = 128 threads.

VOLSIZEX = 512         VOLSIZEY = 512

BLOCKSIZEX = 16        BLOCKSIZEY = 8

UNROLLX = 1

Grid Size in the x dimension = Gsz.x = 512/16 = 32

Grid Size in the y dimension = Gsz.y = 512/8 = 64

Grid Size in the z dimension = UNROLLX = 1

Thus the number of thread blocks issued  = (32, 64)

and the number of blocks in the queue at a given point in time = 32 x 64 = 2048 thread blocks.
