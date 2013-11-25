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

[Here][link] is the RODINIA Benchmark Suite, courtesy of the Department of Computer Science at the University of Virginia.

[link]: https://www.cs.virginia.edu/~skadron/wiki/rodinia/index.php/Main_Page


Other benchmarks used include: AES Cryptography, Graph Algorithm: Breadth First Search, Coulombic Potential, gpuDG, 3D Laplace Solver, LIBOR Monte Carlo, MUMmerGPU, Neural Network Digit Recognition, N-Queens Solver, Ray Tracing, StoreGPU, Weather Prediction, Black-Scholes BLK option pricing, and Fast Walsh Transform.
