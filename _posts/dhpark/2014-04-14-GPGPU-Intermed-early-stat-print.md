---
layout: post
title: "Early Cache Stats Printing in GPGPU-Sim"
description: ""
category: "sphynx"
tags: [blog]
author: dhpark
---
{% include JB/setup %}


Sorry for the delay, but I finally modified the GPGPU-sim code to print early cache statistics so we can adjust for compulsory misses. The original plan was to have all our benchmarks have some sort of a dry-run initially to fill up the cache before collecting data, but looking at the source code, trying to manipulate when/how the benchmarks are run is going to be pretty tricky. So intead, we are settling for printing the cache statistics early (like after first 10,000 cycles), then comparing it with the final cache statistics once everything finishes running.

Read on for details on how the soruce code was modified.



### GPGPU-Sim Source Code Changes

These two files were modified:

 * `gpu-sim.cc`  
 * `gpu-sim.h`  

#### In `gpgpu-sim.cc`

I added a `print_l1_cache_statistics()` function to the `gpgpu_sim` object with the following code:

``` cpp
void gpgpu_sim::print_l1_cache_statistics()
{
   printf("======= INTERMEDIARY CACHE STATS ====== \n");
   shader_print_cache_stats(stdout);
   cache_stats core_cache_stats;
   //core_cache_stats.clear();
   for(unsigned i=0; i<m_config.num_cluster(); i++){
       m_cluster[i]->get_cache_stats(core_cache_stats);
   }
   printf("\nTotal_core_cache_stats:\n");
   core_cache_stats.print_stats(stdout, "Total_core_cache_stats_breakdown");
   printf("======================================== \n");
}

```

This code basically tells the gpgpu-sim object to print the current L1 cache statistics for each core. I had the `cycle()` command call this method. Write now, `cycle()` method simulates a single cycle of gpu execuation, then prints a one-line status every 500-1000 cycles. I inserted this line when in the block of code that prints these statistics so the cache statics get printed after the first 10,000 cycles:

``` cpp
if (gpu_sim_cycle == CACHE_PRINT_CYCLE_COUNT)
	print_l1_cache_statistics();
```

`CACHE_PRINT_CYCLE_COUNT` is set to 10,000 right now.

#### In `gpu-sim.h`

The only change made in this file is to add the function header for the `print_l1_cache_statistics` amongst the public declarations for `gpgpu_sim` object.


#### New Printout:

I tested this using the default `GTX480` configuration for `CP` benchmark.

Here's what we see from the cache statics at 10,000 cycle point:

``` text
GPGPU-Sim uArch: cycles simulated: 10000  inst.: 5276160 (ipc=527.6) sim_rate=439680 (inst/sec) elapsed = 0:0:00:12 / Mon Apr 14 22:23:55 2014
======= INTERMEDIARY CACHE STATS ====== 

========= Core cache stats =========
L1I_cache:
PRINT FORMAT:L1I_cache_core[ Cluster_Index][ Core_index ]: Access, Miss, Miss_rate, Pending_hits, Reservation_fails 

	L1I_cache_core[0][0]: Access = 5943, Miss = 114, Miss_rate = 0.01918, Pending_hits = 0, Reservation_fails = 0
	L1I_cache_core[1][0]: Access = 5966, Miss = 114, Miss_rate = 0.01911, Pending_hits = 0, Reservation_fails = 0
	L1I_cache_core[2][0]: Access = 5938, Miss = 113, Miss_rate = 0.01903, Pending_hits = 0, Reservation_fails = 0
	L1I_cache_core[3][0]: Access = 5969, Miss = 114, Miss_rate = 0.01910, Pending_hits = 0, Reservation_fails = 0
	L1I_cache_core[4][0]: Access = 5978, Miss = 115, Miss_rate = 0.01924, Pending_hits = 0, Reservation_fails = 0
	L1I_cache_core[5][0]: Access = 5964, Miss = 114, Miss_rate = 0.01911, Pending_hits = 0, Reservation_fails = 0
	L1I_cache_core[6][0]: Access = 5934, Miss = 113, Miss_rate = 0.01904, Pending_hits = 0, Reservation_fails = 0
	L1I_cache_core[7][0]: Access = 5941, Miss = 113, Miss_rate = 0.01902, Pending_hits = 0, Reservation_fails = 0
	L1I_cache_core[8][0]: Access = 5910, Miss = 104, Miss_rate = 0.01760, Pending_hits = 0, Reservation_fails = 0
	L1I_cache_core[9][0]: Access = 5895, Miss = 107, Miss_rate = 0.01815, Pending_hits = 0, Reservation_fails = 0
	L1I_cache_core[10][0]: Access = 5894, Miss = 100, Miss_rate = 0.01697, Pending_hits = 0, Reservation_fails = 0
	L1I_cache_core[11][0]: Access = 5904, Miss = 105, Miss_rate = 0.01778, Pending_hits = 0, Reservation_fails = 0
	L1I_cache_core[12][0]: Access = 5902, Miss = 103, Miss_rate = 0.01745, Pending_hits = 0, Reservation_fails = 0
	L1I_cache_core[13][0]: Access = 5885, Miss = 100, Miss_rate = 0.01699, Pending_hits = 0, Reservation_fails = 0
	L1I_cache_core[14][0]: Access = 5890, Miss = 97, Miss_rate = 0.01647, Pending_hits = 0, Reservation_fails = 0
	L1I_total_cache_accesses = 88913
	L1I_total_cache_misses = 1626
	L1I_total_cache_miss_rate = 0.01829
	L1I_total_cache_pending_hits = 0
	L1I_total_cache_reservation_fails = 0
L1D_cache:
	L1D_cache_core[0]: Access = 0, Miss = 0, Miss_rate = -nan, Pending_hits = 0, Reservation_fails = 0
	L1D_cache_core[1]: Access = 0, Miss = 0, Miss_rate = -nan, Pending_hits = 0, Reservation_fails = 0
	L1D_cache_core[2]: Access = 0, Miss = 0, Miss_rate = -nan, Pending_hits = 0, Reservation_fails = 0
	L1D_cache_core[3]: Access = 0, Miss = 0, Miss_rate = -nan, Pending_hits = 0, Reservation_fails = 0
	L1D_cache_core[4]: Access = 0, Miss = 0, Miss_rate = -nan, Pending_hits = 0, Reservation_fails = 0
	L1D_cache_core[5]: Access = 0, Miss = 0, Miss_rate = -nan, Pending_hits = 0, Reservation_fails = 0
	L1D_cache_core[6]: Access = 0, Miss = 0, Miss_rate = -nan, Pending_hits = 0, Reservation_fails = 0
	L1D_cache_core[7]: Access = 0, Miss = 0, Miss_rate = -nan, Pending_hits = 0, Reservation_fails = 0
	L1D_cache_core[8]: Access = 0, Miss = 0, Miss_rate = -nan, Pending_hits = 0, Reservation_fails = 0
	L1D_cache_core[9]: Access = 0, Miss = 0, Miss_rate = -nan, Pending_hits = 0, Reservation_fails = 0
	L1D_cache_core[10]: Access = 0, Miss = 0, Miss_rate = -nan, Pending_hits = 0, Reservation_fails = 0
	L1D_cache_core[11]: Access = 0, Miss = 0, Miss_rate = -nan, Pending_hits = 0, Reservation_fails = 0
	L1D_cache_core[12]: Access = 0, Miss = 0, Miss_rate = -nan, Pending_hits = 0, Reservation_fails = 0
	L1D_cache_core[13]: Access = 0, Miss = 0, Miss_rate = -nan, Pending_hits = 0, Reservation_fails = 0
	L1D_cache_core[14]: Access = 0, Miss = 0, Miss_rate = -nan, Pending_hits = 0, Reservation_fails = 0
	L1D_total_cache_accesses = 0
	L1D_total_cache_misses = 0
	L1D_total_cache_pending_hits = 0
	L1D_total_cache_reservation_fails = 0
	L1D_cache_data_port_util = 0.000
	L1D_cache_fill_port_util = 0.000
L1C_cache:
	L1C_total_cache_accesses = 41886
	L1C_total_cache_misses = 3620
	L1C_total_cache_miss_rate = 0.0864
	L1C_total_cache_pending_hits = 0
	L1C_total_cache_reservation_fails = 4679
L1T_cache:
	L1T_total_cache_accesses = 0
	L1T_total_cache_misses = 0
	L1T_total_cache_pending_hits = 0
	L1T_total_cache_reservation_fails = 0

Total_core_cache_stats:
	Total_core_cache_stats_breakdown[CONST_ACC_R][HIT] = 38266
	Total_core_cache_stats_breakdown[CONST_ACC_R][MISS] = 3620
	Total_core_cache_stats_breakdown[CONST_ACC_R][RESERVATION_FAIL] = 4679
	Total_core_cache_stats_breakdown[INST_ACC_R][HIT] = 87287
	Total_core_cache_stats_breakdown[INST_ACC_R][MISS] = 1626
======================================== 
GPGPU-Sim PTX: 5400000 instructions simulated : ctaid=(7,11,0) tid=(15,1,0)

```

It's a bit concerning that there's no data access during the first 10,000 cycles(???)
And this is the final cache statistic after benchmark is completed

``` text

========= Core cache stats =========
L1I_cache:
PRINT FORMAT:L1I_cache_core[ Cluster_Index][ Core_index ]: Access, Miss, Miss_rate, Pending_hits, Reservation_fails 

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
	L1D_total_cache_accesses = 8192
	L1D_total_cache_misses = 4096
	L1D_total_cache_miss_rate = 0.5000
	L1D_total_cache_pending_hits = 0
	L1D_total_cache_reservation_fails = 5
	L1D_cache_data_port_util = 0.001
	L1D_cache_fill_port_util = 0.001
L1C_cache:
	L1C_total_cache_accesses = 1028096
	L1C_total_cache_misses = 22056
	L1C_total_cache_miss_rate = 0.0215
	L1C_total_cache_pending_hits = 0
	L1C_total_cache_reservation_fails = 5482
L1T_cache:
	L1T_total_cache_accesses = 0
	L1T_total_cache_misses = 0
	L1T_total_cache_pending_hits = 0
	L1T_total_cache_reservation_fails = 0

Total_core_cache_stats:
	Total_core_cache_stats_breakdown[GLOBAL_ACC_R][HIT] = 28
	Total_core_cache_stats_breakdown[GLOBAL_ACC_R][MISS] = 4068
	Total_core_cache_stats_breakdown[GLOBAL_ACC_R][RESERVATION_FAIL] = 5
	Total_core_cache_stats_breakdown[CONST_ACC_R][HIT] = 1006040
	Total_core_cache_stats_breakdown[CONST_ACC_R][MISS] = 22056
	Total_core_cache_stats_breakdown[CONST_ACC_R][RESERVATION_FAIL] = 5482
	Total_core_cache_stats_breakdown[GLOBAL_ACC_W][HIT] = 4068
	Total_core_cache_stats_breakdown[GLOBAL_ACC_W][MISS] = 28
	Total_core_cache_stats_breakdown[INST_ACC_R][HIT] = 2072576
	Total_core_cache_stats_breakdown[INST_ACC_R][MISS] = 1745

```
