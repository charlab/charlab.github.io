---
layout: post
title: "SPHYNX Benchmark List"
description: ""
category: "sphynx"
tags: [blog]
author: dhpark
---
{% include JB/setup %}

Last Update: 2/17/2014 7:30PM


This blog post will keep a table of all the benchmarks & machine configurations that have been simulated and saved on Charlab machine. Update this table once the benchmark is run & the appropriate output files are moved into the results directory.


The output file of the benchmark will be saved in `/data/charlab/gpgpu-sim/RESULTS/` directory.



| Machine                       |  BFS  |   CP  |  LIB  |  LPS  |   NN  |  NQU  |  RAY  |  STO  |
| ----------------------------- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| GTX 480 default [4:64:4]      |  X    |   X   |   X   |   X   |   X   |   X   |   X   |   X   |
| Quadro FX5600 default         |  X    |   X   |   X   |   X   | Error |   X   |   X   |   X   |
| Quadro FX5800 default         |       |       |       |       |       |       |       |       |
| Tesla C2050 default           |       |       |       |       |       |       |       |       |
| _____________________________ |_______|_______|_______|_______|_______|_______|_______|_______|
| GTX480 Unified Cluster        |       |   X   |       |       |       |       |       |       |
| GTX480 Unified Core [4:64:4]  |   X   |   X   |   X   |   X   | Error |   X   |   X   |   X   |
| GTX480 Unified Core [60:64:4] |       |       |       |       |       |       |       |       |
|                               |       |       |       |       |       |       |       |       |
|                               |       |       |       |       |       |       |       |       |
|                               |       |       |       |       |       |       |       |       |

--

The `[#:#:#]` following each GPU is the per-core L1 Instruction cache configuration. The tag goes as: `[ NumSet : BlockSize : Associativity ] `
 
 
__Notes__
*  `GTX 480 default` and `Quadro FX5600 default` were not run with the modified L1 cache print.  
*  `GTX480 Unified Cluster` is GTX480 with all the cores moved to a single cluster.  
*  `GTX480 Unified Core` is single-core configuration of GTX480. Its cache size was not changed reflect the increased execution width.  

 

Runtime observations: `LIB` seems to take an extremely long time to finish (~1hour or more). On the other hand, `NQU` is very short (~6 second simulation time). 










