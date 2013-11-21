---
layout: post
title: "GPGPU-sim Setup Instructions"
description: ""
category: "sphynx"
tags: [Tera, gpgpu-sim, blog]
author: dhpark
---
{% include JB/setup %}

<<<<<<< `WORK IN PROGRESS` >>>>>>

Here are the instructions for setting up the GPGPU-sim to build successfully in Tera, with the `CUDA Toolkit`.
**I'm still having trouble getting the `CUDA SDK` to work properly**
For now, the only thing that is working is building the GPGPU-sim with the `make` command. 
The `CUDA SDK` is required to run the example codes, but I am having trouble getting `CUDA SDK` up and running with the code.

**SETTING UP GPGPU-SIM**

1. Login to Tera and setup git in your repository.
2. Pull the GPGPU-sim code from the charlab repository. See instructions from my previous posts.
3. Go to `gpgpu-sim/v3.x` directory.
4. Look through `README` file. It should give you a general idea of what needs to be done.
5. Go open `~/.bashrc` file. (~/ refers to your top-level home directory)
6. Add in these two lines to the file:

```
export CUDA_INSTALL_PATH=/usr/local/cuda
export PATH=$PATH:$CUDA_INSTALL_PATH/bin
```

7. 

