---
layout: post
title: "GTX580 and How to Config in GPGPU-Sim"
description: ""
category: "sphynx"
tags: [blog]
author: dhpark
---
{% include JB/setup %}


### Introducing GTX580!

This is the fully unlocked version of `GTX480` that have been provided by GPGPU-Sim. The only real difference is that we are going from 15 SM cores to 16 SM cores. This is done by setting `gpgpu_n_clusters` parameter in the config file, and everything else remains the same.


### How to Configure GPU Cores to share L1I cache

There are two files that need to be changed:

 * `gpgpusim.config`  
 * `config_fermi_islip.icnt`  

Considering how default GTX580 has total of 16SM cores, let `NSCALE` be the number of SM cores we want to group together. (ex. if `NSCALE = 2`, we are having every two cores share a signle L1I, resulting in 8 total L1I caches)

Remember that we are having the cores share common caches by merging cores together and scaling a single core to match the pipeline of several cores


#### In `gpgpusim.config`

Here's the list of parameters that need to be changed:

 * `gpgpu_n_clusters 16/NSCALE` - Number of SIMT clusters  
 * `gpgpu_shader_registers 32768*NSCALE` - Number of Shader Core registers  
 * `gpgpu_shader_core_pipeline 1536*NSCALE:32` - Number of threads in the pipeline  
 * `gpgpu_shader_cta 8*NSCALE` - Number of Cooperative Thread Arrays per shader core  
 * `gpgpu_num_sched_per_core 2*NSCALE` - Number of schedulers per core  
 * `gpgpu_cache:il1` - Instruction cache architecture  


`gpgpu_n_clusters` - For cores to share instruction cache, we need them to be in the same cluster, so we reduce the cluster count by how many caches there are.

`gpgpu_shader_registers` - Each core contains 32768 registers, so scale it by number of cores we want to represent.

`gpgpu_shader_core-pipeline` - Each Fermi core contains 1536 threads, so scale that by NSCALE. 32 is the number of threads per warp. (resulting in 48 warps per core)

`gpgpu_shader_cta` - Each Fermi core contains 8 CTA, so scale it by NSCALE.

`gpgpu_num_sched_per_core` - Each Fermi core has two schedulers, so we scale that by NSCALE.


Finally, we configure `gpgpu_cache:il1` based on the cache architecture we want to simulate. We have discussed this on a previous blog post.


#### In `config_fermi_islip.icnt`

There's only one thing that needs to be changed in this file.

 * `k = 28` - This is the topology of the simulated GPU.  

This variable defines the [Topology configuration](http://gpgpu-sim.org/manual/index.php5/GPGPU-Sim_3.x_Manual#Topology_Configuration). `k` should equal `gpgpu_n_clusters + gpgpu_n_mem*gpgpu_n_sub_partition_per_mchannel` from `gpgpu_config`. For GTX580 configuration, since `n_mem = 6` and `sub_partition = 2`, we need `k = n_clusters + 12`.



### Current status of testing:

These are the cache parameters that have been simulated for each core configuration.  
The L1I configurations are specified as: `SetNum_BlockSize_Associativity`

 * 01SM
   * `1_128_24` , `1_128_32`
   * `2_128_24` , `2_128_4` , `2_128_16` `2_128_32`
   * `4_128_2` , `4_128_4` , `4_128_6` , `4_128_8` , `4_128_10` ,  `4_128_12` , `4_128_14` , `4_128_16` , `4_128_20` , `4_128_24` , `4_128_32` 
   * `6_128_4`
   * `8_128_4` 
 * 02SM
   * `1_128_32`
   * `2_128_4` , `2_128_16`
   * `4_128_2` , `4_128_4` , `4_128_6` , `4_128_8` , `4_128_10` , `4_128_16`
   * `6_128_4`
   * `8_128_4`
   *  `12_128_4`
   * `16_128_4`
 * 04SM
   * `1_128_4`
   * `2_128_4` , `2_128_16` , `2_128_32` 
   * `4_128_1` , `4_128_2` , `4_128_4` , `4_128_6` , `4_128_8` ,  `4_128_12` , `4_128_10` , `4_128_16` ,  `4_128_24`  
   * `6_128_4`  
   * `8_128_4` 
   * `16_128_4`
 * 08SM
    * `2_128_4`
    * `4_128_2`  , `4_128_4` , `4_128_8` 
    * `8_128_4` 
 * 16SM (default)
   * `2_128_4`
   * `4_128_4`
 

Fabhia's currently processing all the data we got from all the runs.





