---
layout: post
title: "Modification to Instruction Cache Printout"
description: ""
category: "sphynx"
tags: [blog]
author: dhpark
---
{% include JB/setup %}

While working on setting a unified cache configuration, I noticed something annoying about our GPGPU-Sim output. If we look at the part where we get the L1 cache data, we can notice that we don't get a detailed breakdown of how L1 cache in each core performed like we do with the data cache. For example:

```
L1I_cache:  
	L1I_total_cache_accesses = 2074321  
	L1I_total_cache_misses = 1745  
	L1I_total_cache_miss_rate = 0.0008  
	L1I_total_cache_pending_hits = 0  
	L1I_total_cache_reservation_fails = 0  
L1D_cache:  
	L1D_cache_core[0]: Access = 544, Miss = 272, Miss_rate = 0.500, Pending_hits = 0, Reservation_fails = 0  
	L1D_cache_core[1]: Access = 544, Miss = 272, Miss_rate = 0.500, Pending_hits = 0, Reservation_fails = 0  
	L1D_cache_core[2]: Access = 544, Miss = 272, Miss_rate = 0.500, Pending_hits = 0, Reservation_fails = 0  
	L1D_cache_core[3]: Access = 544, Miss = 272, Miss_rate = 0.500, Pending_hits = 0, Reservation_fails = 0  
	L1D_cache_core[4]: Access = 544, Miss = 272, Miss_rate = 0.500, Pending_hits = 0, Reservation_fails = 0  
	L1D_cache_core[5]: Access = 544, Miss = 272, Miss_rate = 0.500, Pending_hits = 0, Reservation_fails = 0  
	L1D_cache_core[6]: Access = 544, Miss = 272, Miss_rate = 0.500, Pending_hits = 0, Reservation_fails = 0  
	L1D_cache_core[7]: Access = 544, Miss = 272, Miss_rate = 0.500, Pending_hits = 0, Reservation_fails = 0  
	L1D_cache_core[8]: Access = 544, Miss = 272, Miss_rate = 0.500, Pending_hits = 0, Reservation_fails = 0  
	L1D_cache_core[9]: Access = 544, Miss = 272, Miss_rate = 0.500, Pending_hits = 0, Reservation_fails = 0  
	L1D_cache_core[10]: Access = 544, Miss = 272, Miss_rate = 0.500, Pending_hits = 0, Reservation_fails = 5  
	L1D_cache_core[11]: Access = 576, Miss = 288, Miss_rate = 0.500, Pending_hits = 0, Reservation_fails = 0  
	L1D_cache_core[12]: Access = 544, Miss = 272, Miss_rate = 0.500, Pending_hits = 0, Reservation_fails = 0  
	L1D_cache_core[13]: Access = 544, Miss = 272, Miss_rate = 0.500, Pending_hits = 0, Reservation_fails = 0  
	L1D_cache_core[14]: Access = 544, Miss = 272, Miss_rate = 0.500, Pending_hits = 0, Reservation_fails = 0  
```

As you can see, the statistics for instruction cache is jumbled up in a single statistic, while data cache gets a breakdown of how each core performed. I decided to fix this, since getting a breakdown of like we have with the data cache is useful to have, especially for checking whether we have our cache configuration set the way we want.

I'll split this blog into two parts. First part will go straight to the result of the change and how the new output is organized. Second part will go into exactly what I changed in the GPGPU-sim source code.


## New Cache Statistic Output

The new instruction cache statistic for `GTX480` running `CP` benchmark looks like this: (The precision of Miss Rate is also changed to 5 sig figs)

```
L1I_cache:
PRINT FORMAT:L1I_cache_core[Cluster_Index][Core_index]: Access, Miss, Miss_rate, Pending_hits, Reservation_fails  
   
	L1I_cache_core[0][0]: Access = 137754, Miss = 122, Miss_rate = 0.00089, Pending_hits = 0, Reservation_fails = 0  
	L1I_cache_core[1][0]: Access = 137754, Miss = 122, Miss_rate = 0.00089, Pending_hits = 0, Reservation_fails = 0  
	L1I_cache_core[2][0]: Access = 137754, Miss = 122, Miss_rate = 0.00089, Pending_hits = 0, Reservation_fails = 0  
	L1I_cache_core[3][0]: Access = 137753, Miss = 121, Miss_rate = 0.00088, Pending_hits = 0, Reservation_fails = 0  
	L1I_cache_core[4][0]: Access = 137756, Miss = 124, Miss_rate = 0.00090, Pending_hits = 0, Reservation_fails = 0  
	L1I_cache_core[5][0]: Access = 137754, Miss = 122, Miss_rate = 0.00089, Pending_hits = 0, Reservation_fails = 0  
	L1I_cache_core[6][0]: Access = 137753, Miss = 121, Miss_rate = 0.00088, Pending_hits = 0, Reservation_fails = 0  
	L1I_cache_core[7][0]: Access = 137753, Miss = 121, Miss_rate = 0.00088, Pending_hits = 0, Reservation_fails = 0  
	L1I_cache_core[8][0]: Access = 137744, Miss = 112, Miss_rate = 0.00081, Pending_hits = 0, Reservation_fails = 0  
	L1I_cache_core[9][0]: Access = 137746, Miss = 114, Miss_rate = 0.00083, Pending_hits = 0, Reservation_fails = 0  
	L1I_cache_core[10][0]: Access = 137740, Miss = 108, Miss_rate = 0.00078, Pending_hits = 0, Reservation_fails = 0  
	L1I_cache_core[11][0]: Access = 145841, Miss = 113, Miss_rate = 0.00077, Pending_hits = 0, Reservation_fails = 0  
	L1I_cache_core[12][0]: Access = 137743, Miss = 111, Miss_rate = 0.00081, Pending_hits = 0, Reservation_fails = 0  
	L1I_cache_core[13][0]: Access = 137739, Miss = 107, Miss_rate = 0.00078, Pending_hits = 0, Reservation_fails = 0  
	L1I_cache_core[14][0]: Access = 137737, Miss = 105, Miss_rate = 0.00076, Pending_hits = 0, Reservation_fails = 0  
	L1I_total_cache_accesses = 2074321  
	L1I_total_cache_misses = 1745  
	L1I_total_cache_miss_rate = 0.00084  
	L1I_total_cache_pending_hits = 0  
	L1I_total_cache_reservation_fails = 0  
```

As you can see, we have `Cluster_Index` followed by `Core_index`. In GPGPU-Sim, we have `SIMT Core Clusters` which are analogous to NVIDIA's `Streaming Multiprocessors` and AMD's `Compute Unit`. Each of these clusters can contain multiple `SIMT Cores` (or `shader cores`) as you can see in the image below.For the default configuration of `GTX480`, we have 15 SIMT Core Clusters, with only one core per cluster. Note that these `SIMT Cores` are __NOT__ the same as so-called `CUDA Cores`. 

![GPGPU-Sim Arch](http://gpgpu-sim.org/manual/images/2/21/Overall-arch.png)



## Tweaking GPGPU-Sim Source Code
Here are the steps I took to tweak the output format of instruction cache statistics. There were two files that needed to be tweaked. `src/gpgpu-sim/shader.cc` and `src/gpgpu-sim/shader.h`.

#### In `shader.cc`

At line 1985, we have the `shader_print_cache_stats` function in `gpgpu-sim` class that gets called during the final output phase of GPGPU-Sim. This function goes through each L1 cache type (I,D,C,T) and prints the stats for each. The instruction cache portion of this function was modified to:

{% highlight c++ %}
fprintf( stdout, "PRINT FORMAT:L1I_cache_core[ Cluster_Index][ Core_index ]: Access, Miss, Miss_rate, Pending_hits, Reservation_fails \n\n");
	for ( unsigned i = 0; i < m_shader_config->n_simt_clusters; ++i ) {
	    cluster_css.clear();
	    curr_core = m_cluster[i]->get_core();
	    for ( unsigned j = 0; j < m_shader_config->n_simt_cores_per_cluster; ++j ) {
        	curr_core[j]->get_L1I_sub_stats(css);

		fprintf( stdout, "\tL1I_cache_core[%d][%d]: Access = %d, Miss = %d, Miss_rate = %.5lf, Pending_hits = %u, Reservation_fails = %u\n",
                     i,j, css.accesses, css.misses, (double)css.misses / (double)css.accesses, css.pending_hits, css.res_fails);

        	cluster_css += css;
    	    }i    
            total_css += cluster_css;
        }
{% endhighlight %}

The code essentially goes through each core of each cluster to gather and print the cache necessary statistics.

#### In `shader.h`

One slight problem in looping through each core was that the pointer to the `shader core` array in each cluster was a private variable that couldn't be accssed by the `gpgpu-sim` class. The simplest solution to this problem (though not really the safest) was to add a `get_core()` function.

(% highlight c++ %}
    shader_core_ctx **get_core() { return m_core; }
{% endhighlight %}


