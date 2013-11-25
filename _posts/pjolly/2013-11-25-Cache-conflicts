---
layout: post
title: "Cache Conflicts"
description: ""
category: "Threads"
tags: [tutorial, blog, jekyll]
author: pjolly
---
{% include JB/setup %}


This week, I researched about common inter-thread conflicts that occur and summarized the proposed solution by a paper published by Sato et al. from Tohoku University. Two common conflicts are inter-thread kick out (ITKO) and capacity shortages. The former is the one we are more familiar with: cached data desired by a specific thread has already been evicted by another thread resulting in increased execution time for the second thread. For capacity shortages, if the total capacity required by all the threads accessing the cache exceeds the total capacity of the cache, the different threads end up competing for the limited space.
Performance with respect to these conflicts can be evaluated by looking at the relative throughputs. Multi-threading programs thread performance are compared to the same threads in a single-thread program. If, after the change added for multithreading, the throughput decreases from 100%, we can see through a simple cost benefit analysis whether the costs of inter-thread conflict outweigh the benefits of multithreading. 
In terms of solutions, previously, dynamic cache partitioning has been proposed to solve the ITKO conflicts, however this presents a significant trade off in terms of capacity shortages. By partitioning the cache to groups of threads, the capacity space would be even more limited and would therefore result in a degradation of performance due to lack of space. Sato et al. proposed a "Cache-aware thread scheduling policy" that actually profiles the number of ways requested by a thread and then partitions the cache intelligently between them. With this scheduling policy, a high cache requirement thread can be paired with a low cache requirement thread which would help prevent capacity shortages as well as ITKOs. The team proposed some algorithms for measuring the cache requirement of various threads and for choosing automatically how to partition the cache for various programs.

Note on Experimentation: 
- Using an M5 simulator, they evaluated the effectiveness of their algorithm
- Six benchmark programs selected from the SPEC CPU2000 benchmark suite to cover a range of combinations of cache accesses etc.
- Conclusion: performance improves by a maximum of 10% and an average of around 5% compared to worst case thread scheduling
- Drawbacks: profiling method used in the paper is high-cost
