---
layout: post
title: "GPGPU-sim Working Benchmark"
description: ""
category: "sphynx"
tags: [Tera, gpgpu-sim, blog]
author: dhpark
---
{% include JB/setup %}

After a long-long series of guessing, googling, text scrambling and copy&pastes, Akhil and I finally managed to get *some* of the example benchmarks in GPGPU-sim to build, and **ONE** benchmark to run successfully without giving us any segfaults. I'll add a blog post on how to add CUDA SDK into your directory later in the week. (probably by putting it on a GIT repository) There were a ton of semi-random, non-intuitive hacks we had to do to get the example code compiling, but hopefully we will be able to get it to work on everyone's directory.  

Out of 12 total benchmarks that came with GPGPU-sim, the ones scratched out are the ones that failed to compile, and the one in *bold* is the one that successfully compiled. 

{% highlight text %}  

* ~~AES~~ 
* BFS
* **CP**
* ~~DG~~
* LIB
* LPS
* ~~MUM~~
* NN
* NQU
* ~~RAY~~
* STO
* ~~WP~~
{% endhighlight %}

We ran the `CP` benchmark successfully with a simulation of GTX480. We didn't try the other GPUs that came with GPGPU-sim, but it should work in the similar manner. 

Here is a description of the `CP` benchmark from the paper on [GPGPU-sim](http://www.ece.ubc.ca/~aamodt/papers/gpgpusim.ispass09.pdf)

{% highlight text %}  

**Coulombic Potential (CP)**  
CP is part of the Parboil
Benchmark suite developed by the IMPACT research group at
UIUC [18,41]. CP is useful in the ﬁeld of molecular dynamics.
Loops are manually unrolled to reduce loop overheads and
the point charge data is stored in constant memory to take
advantage of caching. CP has been heavily optimized (it
has been shown to achieve a 647× speedup versus a CPU
version)  

{% endhighlight %}

You can see the output files from running the benchmark in the Github directory under `charlab.github.io/_posts/dhpark/`.  
There is `GTX480out.txt`, which is the output file from running `CP` with GTX480. If you look towards the end, there are lot of useful informations like cache misses and runtime.  
The `gpgpusim_power_report_Mon-Dec--2-00-40-37-2013.log` is the log file of the simulation power consumption from running the benchmark. It reported an average power consumption of 99.50 (W?) and max power of 142 (W?). 


