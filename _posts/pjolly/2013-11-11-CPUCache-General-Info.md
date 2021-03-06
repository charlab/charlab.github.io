---
layout: post
title: "CPU Cache General Info"
description: ""
category: "Caches"
tags: [sphynx, caches]
author: pjolly
---
{% include JB/setup %}

The CPU cache stores copies of data from frequently used memory locations. This allows the run time of the CPU to be much shorter since drawing/reading memory from the main memory locations requires more time. The cache memory is always a first step for the CPU when writing or reading data. If the data being written/read is already present in the cache, it does not need to access main memory which saves time.

Three main types of caches:

- **Instruction Cache**: easy access to instruction data
- **Data Cache**: easy access to data
- **Translation Lookaside Buffer (TLB)**: used to speed up virtual-physical memory translation for both the above caches

If the cache is full, the processor decides which cache entry to replace based on "Replacement Policies." A common replacement policy is least-recently used (LRU): data entry that is the least recently accessed is replaced.

Terms:

- **Cache line**: segments of fixed size in which data is transferred between memory and cache
- **Cache hit**: the processor finds something it needs in the cache
- **Cache miss**: needed data not present in cache; a new entry with needed data is consequently created (data needed is copied from main memory into cache)
- **Hit rate**: number of cache hits divided by total number of accesses; used to measure cache performance
- **CPU stalls**: state when the CPU is waiting for a cache line to be fetched from memory (read latency). During this stall time, the CPU could potentially complete many other computations. So, stalling can slow down computer significantly.
- **Multi-threading**: using multiple threads to access cache; This can speed up CPU run time because another thread can use the CPU core while the first thread waits for data from the main memory (avoiding stall).
- **Cache Size**: amount of main memory it can hold = Num. bytes in Data block*Num. of cache blocks (See "Cache Entry Structure Below")

Cache Entry Structure (One cache block):

```
| Tag | Data Block | Flag Bits |
|:---:|:----------:|:---------:|
```

**Tag**: part of the address location of data in main memory

**Data Block**: Actual data fetched from main memory

**Flag Bits**: one bit the indicates whether or not there is a valid entry in the cache block (whether cache block is used) 
