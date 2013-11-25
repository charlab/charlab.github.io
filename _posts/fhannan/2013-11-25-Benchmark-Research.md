---
layout: post
title: "Benchmark Research"
description: ""
category: "blog"
tags: [blog, jekyll]
author: fhannan
---
{% include JB/setup %}


Terminology (including terms from last week):

- logical page: contains more data than can fit on the physical page

- direct-mapped cache: each memory location is mapped to one specific cache entry location

- fully associative cache: each memory location can be mapped to any cache entry location

- two-way set associative cache: each memory location can be mapped to only one of two cache entry locations

- kernel: grid of blocks of warps of scalar threads

- warp: groups of threads in hardware meant to execute in lockstep

- SIMT: Single Instruction, Multiple Thread, coined by NVIDIA to describe their GPU CUDA architecture

- ISA: instruction set architecture

- SASS: Native ISA for NVIDIA GPUs

- PTX: Parallel Thread eXecution; NVIDIA's scalar, low-level, and data-parallel virtual ISA

__

[This powerpoint][ppt] had a lot of useful information on and good explanations of GPGPU-Sim: "GPUWattch + GPGPU-Sim: An Integrated Framework for Performance and Energy Optimizations in Manycore Architectures" by Jingwen Leng (The University of Texas at Austin) and Tayler Hetherington (University of British Columbia).

[ppt]: http://gpuwattch.ece.utexas.edu/resources/workshop/ispass-2013/slides/ISPASS_Tutorial_GPGPUSIM.pdf

- I read up on how GPUGU-Sim supports both CUDA and OpenCL.

- The purpose of the presentation is to describe what GPGPU-Sim simulates, show how to setup and run CUDA (the paper focused on CUDA) applications on it, and provide a foundation for research groups.

- It has some information on OpenCL supported GPUs, such as Qualcomm's Adreno 3xx GPU, ARM's Mali-T600 Series GPUs, Intel Ivy Bridge's HD 4000, the Intel Xeon Phi (Knights Corner), NVIDIA Quadro FX 5800, NVIDIA Tesla C2050 (Fermi), and NVIDIA GTX 480.

- It also has useful graphs for when the RODINIA Benchmark Suite. Accuracy was measured through functional, computing time, and power models; these are what the GPGPU-Sim is supposed to simulate.

[Here][link] is the RODINIA Benchmark Suite, courtesy of the Department of Computer Science at the University of Virginia. It has descriptions on the site.

[link]: https://www.cs.virginia.edu/~skadron/wiki/rodinia/index.php/Main_Page

In [this paper][paper], "Analyzing CUDA Workloads Using a Detailed GPU Simulator" by Ali Bakhoda, George L. Yuan, Wilson W. L. Fung, Henry Wong and Tor M. Aamodt at the University of British Columbia, they use the following benchmarks:

[paper]: http://www.ece.ubc.ca/~aamodt/papers/gpgpusim.ispass09.pdf

-AES Cryptography/Encryption: uses the Advanced Encryption Standard algorithm in CUDA to encrypt and decrypt files.

-Graph Algorithm: Breadth First Search: breadth first search on a graph

-Coulombic Potential: unroll loops to reduce loop overheads and store point charge data in constant memory with caching

-gpuDG: calculate 3D radar scattering and analyze waves and particle accelerators in electromagnetics

-3D Laplace Solver: parallel finance application; uses shared memory and coalesced global memory accesses

-LIBOR Monte Carlo: Monte Carlo simulations based on the London Interbank Offered Rate Market Model

-MUMmerGPU: matches query strings of standard DNA nucleotides to a reference string to simulate genetic processes

-Neural Network Digit Recognition: recognize handwritten digits withthe network and pre-determined neuron weights and input digits in global memory

-N-Queens Solver: solves a chess board puzzle by placing N queens so that they cannot catch each other

-Ray Tracing: rendering graphics with near photo-realism using scalar threads in CUDA for each pixel

-StoreGPU: accelerates hashing-based primited for middleware

-Weather Prediction: uses the GPU to accelerate a portion of the Weather Research and Forecast Model

-Black-Scholes BLK option pricing: not explained

-Fast Walsh Transform: not explained


Here are other benchmarks I found:

- [Benchmarks used in a 2009 ISPASS paper without explanations of the benchmarks][a]
  [a]: https://dev.ece.ubc.ca/projects/gpgpu-sim/changeset/ba7eeab1ef435177fdfdd264803e18c2208bb57a/ispass2009-benchmarks/benchmarks/README.ISPASS-2009

- [a]
