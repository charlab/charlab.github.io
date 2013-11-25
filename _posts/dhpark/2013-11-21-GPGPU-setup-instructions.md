---
layout: post
title: "GPGPU-sim Setup Instructions"
description: ""
category: "sphynx"
tags: [Tera, gpgpu-sim, blog]
author: dhpark
---
{% include JB/setup %}


Here are the instructions for setting up the GPGPU-sim to build successfully in Tera, with the `CUDA Toolkit`.

**I'm still having trouble getting the `CUDA SDK` to work properly**

For now, the only thing that is working is building the GPGPU-sim with the `make` command. 
The `CUDA SDK` is required to run the example codes, but I am having trouble getting `CUDA SDK` up and running with the code.

**SETTING UP GPGPU-SIM**  
* Login to Tera and setup git in your repository.  
* Pull the GPGPU-sim code from the charlab repository. See instructions from my previous posts.  
* Go to `gpgpu-sim/v3.x` directory.  
   `cd gpgpu-sim/v3.x`

* Look through `README` file. It should give you a general idea of what needs to be done.  
   `gedit README`  
* Open `~/.bashrc` file with a text editor. I recommend `gedit` if you are not familar with linux. (~/ refers to your top-level home directory)  
   `gedit ~/.bashrc`  
* Add in these two lines to the file: 
  
`export CUDA_INSTALL_PATH=/usr/local/cuda`  
`export PATH=$PATH:$CUDA_INSTALL_PATH/bin`  
  

* Now we should be ready to build. Type the following commands on the terminal:  
  
`[dhpark@tera v3.x]$ source setup_environment`  
`[dhpark@tera v3.x]$ make`  
  

* Wait a couple minutes. Don't get intimidated by all the text and warnings that shows up. If something fails, try running `make` again. (It might succeed the second time!)  
* If all goes well, you should see no warnings when the command finishes.
