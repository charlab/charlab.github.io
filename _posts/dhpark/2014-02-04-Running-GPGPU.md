---
layout: post
title: "How to run GPGPU-Sim on Charlab Machine"
description: ""
category: "sphynx"
tags: [blog]
author: dhpark
---
{% include JB/setup %}

Here are the steps on how to setup and run GPGPU-Sim on charlab machine.  
Before we begin, here is the summary of current gpgpu-sim setup on Charlab machine. (`charlab.eng.hmc.edu`)  
`GPGPU-sim` is located on `/data/charlab/gpgpu-sim`. This is where gpgpu-sim will be located at all times. The version of CUDA that is compatible with the current build of GPGPU-sim is **CUDA-4.4**. The `CUDA-4.4 Toolkit` is located in `/data/charlab/cuda`. For running GPGPU-sim, we need always refer to this particular version of cuda. This is different from the CUDA-5.5 located in `/usr/local/cuda/`. The `NVIDIA Computing SDK v4.0` is located in `/data/charlab/NVIDIA_GPU_Computing_SDK`. This SDK is required for compiling the `ispass2009` benchmarks that came with GPGPU-Sim.  

Now here the steps you need to follow for running the benchmarks:  
* Open `~/.bashrc` with a text editor. (`gedit`, `nano`, etc). Add these lines into the file and save it.
```  
export NVIDIA_COMPUTE_SDK_LOCATION=/data/charlab/NVIDIA_GPU_Computing_SDK  

export CUDA_INSTALL_PATH=/data/charlab/cuda  

export PATH=$PATH:$CUDA_INSTALL_PATH/bin  

export LD_LIBRARY_PATH=/data/charlab/cuda/lib64:$LD_LIBRARY_PATH  
```  

* Now go to the GPGPU-Sim directory: `cd /data/charlab/gpgpu-sim/gpgpu-sim/v3.x`  

* Use `source setup_environment` to setup gpgpu-sim to make you use the simulated gpu instead of the actual machine.

* Go to the benchmark directory. `cd /data/charlab/gpgpu-sim/gpgpu-sim/ispass2009-benchmarks/`  

* If it hasn't been setup yet, use `./setup_config.sh <MACHINE>` to get the benchmarks ready to run on GPGPU-Sim. This links the configuration files of a particular <MACHINE> with the directory of each benchmarks. Current machines that are supported are: `GTX480, `QuadroFX5600`, `QuadroFX5800`, and `TeslaC2050`.  

* Pick one of the working benchmarks and go to its directory. Benchmarks that are currently working are:  
'BFS', 'CP', 'LIB', 'LPS', 'NN', 'NQU', 'RAY', 'STO'.  
For example, to run CP, go `cd CP/`

* If you are running GTX480, make sure `gpuwattch_gtx480.xml` file is there. If not, copy the file onto the directory with: `cp ../../v3.x/config/GTX480/gpuwattch_gtx480.xml . `

* Run the benchmark with `sh README.GPGPU-Sim` command. To save the output onto a text file, I recommend using `sh README.GPGPU-Sim > CP_GTX480_out.txt &`. 

* Once you are done running all the benchmarks, youo wanted to test, go to the top-level directory `../ispass2009-benchmarks/` make sure you cleanup the setting by running `./setup_config.sh --cleanup` .












