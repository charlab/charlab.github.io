---
layout: post
title: "Cache Configuration: Take 1"
description: ""
category: "sphynx"
tags: [gpgpu, sphynx]
author: abagaria
---
{% include JB/setup %}

This week Dong-hyeon and I set out to fiddle with the config files. The config file is long and seemed
a little intimidating to me. This was partly because the file was filled with terms I did not understand, magic
numbers and was insufficiently commented. However, looking at the comments in the output file from running the benchmarks 
actually told us much more about the structure of the configuration!

Last semester we spoke about employing the'naive method.' This method being simulating and testing a instruction cache configuration in 
configuration in which all the cores share the same instruction cache as opposed to each core using its own instruction cache.
We thus hoped to, in the best case scenario figure out how to to this, or simply gain some familiarity with the 
config files.

Here is a list of thngs we looked at: 

1. We first looked at the config file to see what we need to change. The line where its all happening is the one which defines
the structure of the L1 Instruction Cache (er shader core). This corresponds to the line which reads `-gpgpu_cache:1l1`

2. The number of SIMT Core Clusters: `-gpgpu_n_clusters`

3. Number of SIMD Cores per Cluster: `gpgpu_n_cores_per_cluster`

4. Number of warp/thread per SIMT core: `gpgpu_shader_core_pipeline`. It seems like Shader Core = SIMT Core.

Since we could not figure out how to affect the change that we were hoping to affect, we set ourselves the task of 
manipulating easier to manipulate configurations and see the result on the output files. 

To this end, we changed the associativity of the cache from 4 to one. This had no observable change on the hit/rate,
which we were expecting to see. 

We then fiddled with the block size and reduced the size from 128 to 64. We expected the miss rate to go up as a 
consequence. Here is the output of running the BFS benchmark with the old block size:

```
===BFS_GTX480== bsize=128
L1I_cache:
	L1I_total_cache_accesses = 19521
	L1I_total_cache_misses = 962
	L1I_total_cache_miss_rate = 0.0493
	L1I_total_cache_pending_hits = 0
	L1I_total_cache_reservation_fails = 6682
```

And here is the output from running BFS with the new reduced block size:

```
===BFS_GTX480_mod= bsize=64===
L1I_cache:
	L1I_total_cache_accesses = 20004
	L1I_total_cache_misses = 1445
	L1I_total_cache_miss_rate = 0.0722
	L1I_total_cache_pending_hits = 0
	L1I_total_cache_reservation_fails = 7088
==============================
```

As is evident, we did see a rise in miss rate as we had expected. Although this was reassuring, we 
still have a lot to understand when it comes to the config file. More specifically, we need to 
first understand where the multiple core-multiple cache configuration is defined. Second, we 
need to figure out a way to change this configuration to a multi core single cache configuration. 
This might entail changing the config of the data cache as well as we suspect that there might be some 
dependence between the data and instruction caches. 

Dong-hyeon will be posting a how-to blog later. Hope this blog was informative and interesting!

- The Legendary Dong-hyeon and Akhil.
