---
layout: post
title: "Architectures"
description: ""
category: "sphynx"
tags: [gpgpu, sphynx]
author: abagaria
---
{% include JB/setup %}

In this blog, I have detailed some relavant stats about some of the more recent architectures.
These stats are in the form of SM Block Diagrams and hardware specifications in tables. 
All the information used to compile this blog has been taken from NVIDI's white papers 
talking about the respective architectures. 

Since we have been discussing the possibility of shifting to either Kepler or Maxwell, 
I have included a kind-of-qualitative comparison between the 2 architectures.

Comparison between Kepler and Maxwell
--------------------------------------

First, some stats about Kepler. It has 4 warp schedulers, 8 instruction dispatch units,
four 32-wide vector ALUs and another 4 16-wide ALUs.

Since there was some confusion about the terminology:

`Warps`: Warps is an NVIDIA term that refers to a group of 32 threads that execute
together. For the purposes of maximizing confusion, AMD refers to them as `wavefronts.`

`CUDA Cores`: This is merely a marketing term. What we are really looking at are SMs 
or Streaming Multiprocessors.

The Maxwell SM is divided into `quads`. Each quad has a warp scheduler, two dispatch units, a dedicated register file, and single vec32 ALU. Each `quad` also has its own instruction buffer. The quads have their own banks of load/store units, and they also have their own special-function units that handle tricky things like interpolation and transcendentals.

There’s a 64 KB shared memory space for the SMM, which carries over from Fermi and then Kepler, but is no longer called out as L1 cache for compute tasks. It used to be that this space could be configured as 48 KB of shared space and 16 KB of L1 and vice versa. Now that's not necessary, so all 64 KB is used as a shared address space for GPU compute.

Maxwell's control logic and execution resources are more directly associated with one another than in Kepler, and the scale of the SM itself is somewhat smaller. One Maxwell SM has 128 stream processors and eight texels per clock of texture filtering, down by one third and one half, respectively, from Kepler. 

Beyond the SM, the other big architectural change in Maxwell is the growth of the L2 cache. The GM107's L2 cache is 2MB, up from just 256KB in the GK107. This larger cache should provide two related benefits: bandwidth amplification for the GPU's external memory and a reduction in the power consumed by doing expensive off-chip I/O.

[imgur link](http://imgur.com/VF61kFw&V467vo2&kbVnAVI&7n1Psv6&de7sb9B&pB9ApO6&6PftUQ2)

![Maxwell Block Diagram](http://i.imgur.com/V467vo2.png?1)

![Maxwell architecture](http://i.imgur.com/kbVnAVI.png?1)

![Maxwell vs. Kepler](http://i.imgur.com/7n1Psv6.png?1)

![Fermi vs. Kepler](http://i.imgur.com/pB9ApO6.png?1)

![Fermi SM Block Diagram](http://i.imgur.com/6PftUQ2.png?1)
