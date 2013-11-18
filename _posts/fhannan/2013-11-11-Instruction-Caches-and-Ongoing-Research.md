---
layout: post
title: "Instruction Caches and Ongoing Research"
description: ""
category: "blog"
tags: [blog, jekyll]
author: fhannan
---
{% include JB/setup %}

I read about caches, instruction caches, their applications, and ongoing research about them.

First of all, a cache is where on can visibly store data. This makes retrieving data significantly faster. If the correct data is sucessfully retrieved, it is a cache hit. If not, it is a cache miss. If more requests for data can be made from the cache, the performance will be much faster. Caches are usually small for efficiency, especially cost-efficiency. This is alright because referencs generally have locality of reference, or make multiple requests for the same data, as opposed to always requesting different data. The cache should store data frequently accessed from the main memory locations. Thus, average memory access latency should be closer to cache latency than main memory latency.

Caches are frequently used by cache clients, such as a CPU (central processing unit), web browser, operating system, etc.

The CPU cache consists of small memories that are close to or on the CPU, in addition to the main memory, which is not nearly as fast. CPU caches now have three independent caches: instruction caches for faster instruction execution, data caches for faster data storage, and a translation lookaside buffer (TLB) for faster virtual-to-physical address translation of instructions and data. Pipeline CPUs access data from multiple caches for the different points in the pipeline. Cache row entires usually organized like so:

```
tag     	data block      	flag bits
```

The tag is the address of the data in the main memory and the data block is the actual data stored. The instruction cache requires only one flag bit per cache, a valid bit to indicate whether valid data has been stored.

Caches can also be specialized. For example, trace caches store traces of instructions previously accessed and decoded for more bandwidth and less power requirements. Multilevel caches have larger but slower caches as backups for the smaller but faster ones, since hit rates are inversely proportional to latency (longer latency can mean a faster hit rate and vice versa). 

I also read up on research on instruction caches. These topics included instruction cache performance on multithreaded architecture (to decrease conflicts between procedures), instruction cache performances in Online Transacton Processes (OLTP) database workloads (since the misses take up 40% of execution time), and other ways of improving execution time and performance.

[This paper][kumar-tullsen-2002] about instruction cache performance on multithreaded architecture by Rakesh Kumar and Dean M Tullsen at University of California, San Diego in 2002 may prove useful in determining how the caches work:

   [kumar-tullsen-2002]: http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.8.4682&rep=rep1&type=pdf

Also, caches are not to be confused with buffers. Buffers are temporary memory locations that can serve as intermediates when CPU instructions cannot directly address data. Using this addressable memory:

1. requires less transfers
2. allows for an intermediate when direct transfers are not possible
3. gives us a minimum data size for a transfer
