---
layout: post
title: "Setting up GPGPU-sim on Tera"
description: ""
category: "sphynx"
tags: [tera, GPGPU]
author: dhpark
---
{% include JB/setup %}

I wanted a place to compile what I found about how to get GPGPU sim up and running on Tera and make a list of the things that needs to be sort out.

First off, here are the list of dependencies that we need to get installed on linux to build the code(from `README` document). The items in bold are the dpendencies that need to be installed on Tera. Ones not in bold have already been installed. 

{% highlight markdown %}
GPGPU-Sim dependencies:
* gcc
* g++
* make
* **makedepend**
* **xutils**
* bison
* flex
* zlib
* **CUDA Toolkit**
	
GPGPU-Sim documentation dependencies:
* **doxygen**
* **graphvi**
{% endhighlight %}

As shown above, to run GPGPU-sim, we need to have CUDA installed. Unfortunately, Tera do not have CUDA-enabled GPUs and NVDIA dropped support for CUDA emulation on non-CUDA machines starting v3.1. Fortunately, GPGPU-sim supports CUDA version 2.3, 3.1 and 4.0, so CUDA emulation should still work if we install version 2.3.



