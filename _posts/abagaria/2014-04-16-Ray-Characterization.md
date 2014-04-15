---
layout: post
title: "Ray Characterization"
description: ""
category: "sphynx"
tags: [gpgpu, sphynx]
author: abagaria
---
{% include JB/setup %}

Last week, I characterized how parallel `CP` and `RAY` were by examining the CUDA files for both the benchmarks. 
I found that `CP` was more parallel than `RAY` -- which mande it an interesting benchmark to analyze despite its 
small size. 

This week, we wanted to finish our characterization of `RAY` by making it more parallel in software. 
This entailed changing the image size that the Ray Tracer would operate on and the number of thread 
blocks (and consequently the number of threads in the queue at a given time). The following are the
calculations related to the tweaked version of `RAY` which serves as an indicator of the degree of parallelism
with which `RAY` executes on the GPU:

```
Number of threads in each block = 16 x 8 = 128 threads.

Number of thread blocks issued = (512/16, 512/8) = (32, 64)

Thus the number of blocks in the queue at a given time = 32 x 64 = 2048.
```

This ensured that the `RAY` benchmark was executing as parallel in software as the Coulombic Potential 
benchmark in the number of work elements that it was issuing. Given that the `RAY` CUDA file issues more
instructions in its core computation that `CP` does, and that a lot of its instructions (CUDA instructions)
seem to be computationally more expensive, `RAY` can now be treated as both a long program which would 
occupy a significant amount of space in the instruction cache (and hence would not be entirely resident in
the instruction cache) AND would issue those instructions with a high degree of parallelism.

In order to examine the affect of changing the software parallelism issued by Ray, we repeated the 
methodology that Fabiha and DH had employed when they were examining the performance of the different 
benchmarks as a function of the number of SM cores. 
