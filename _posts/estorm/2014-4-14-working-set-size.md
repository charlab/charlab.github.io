---
layout: post
title: "Working set size for traces"
description: ""
category: "spock"
tags: [spock, blog, traces]
author: estorm
---
{% include JB/setup %}

For this week, I modified the simulation to work for on an L1, L2, and L3 data cache, instead of just the L1 cache. After doing some research, I found the typical size and associativity of these caches in an i7 processor. After simulating this, I found that the traces were all resident in the cache. This means that there was no recaching in the L3 cache. To determine a good cache configuration moving forward, it will be useful to know the working set size, which is the amount of memory needed by the trace. 

| Trace | Unique Addresses | 
| ------------ | ------------ |
| is\_omp    | 89677 |
| is\_ser    | 152712 |
| ls         | 30938 |
| lu-hp\_omp | 63831 |
| lu-hp\_ser | 63706 |
| lu\_omp    | 67406 |
| lu\_ser    | 61676 |
| sp\_omp    | 64863 |
| sp\_ser    | 61665 |
| ua\_omp    | 447338 |
| ua\_ser    | 567667 |


