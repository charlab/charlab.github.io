---
layout: post
title: "Instruction Cache Metrics"
description: ""
category: "sphynx"
tags: [gpu, sphynx, gpgpu]
author: estorm
---
{% include JB/setup %}

## Instruction Cache Metrics

This week Fabiha, Paul, and I worked on developing metrics to characterize an instruction cache's behavior during execution of a program. 

When creating metrics, we did our best to create metrics that would be applicable for a wide range of potential instruction cache structures. 

### Metrics
##### Instructions loaded per cycle: 
the average number of instructions loaded into the cache would be a measurement of how much the cache is being used. By running identical programs with different cache configurations, a relative comparison will allow the effectiveness of one cache scheme to another.

##### Average instruction read time: 
Depending on the associativity of the instuction cache, it will take more or less time to lookup a value in the instuction cache. This may result in significant speedups or delays. 

##### Stalls due to instuction cache: 
Ultimately, it may be ok if the instuction cache is behaving inefficiently if it means that it reduced the delays stalls in the instruction pipeline. 

##### Instruction Duplication: 
This is a measure of the duplication of instructions. If the same instruction is repeatedly being issued, then the GPU may not be operating in parallel as well as it could be. 

##### Average time to recache:
The average number of cycles that a cache line stays out of the cache before being recached. This is a measure of the effectiveness of the caching scheme because if instructions stay out of the cache for longer periods of time, then the cache is not thrashing. 

## GPGPU-Sim 
I cloned GPGPU-Sim onto my tera account and compiled it. The first time I compiled, it failed with an error, but I ran `make clean` and re-made it and it worked correctly. I was going to try to make the tests, but I couldn't figure out where to set the path to the NVIDIA GPU Computing SDK. 

## New Paper
I started working on a project that some Mudders worked on last year relating to data caches. The research focuses on evaluating caching strategies for data caches in CPUs. They ran a program with five different cache replacement strategies. In the study, they used a single cache structure and program and varied the replacement strategies. They used an 8-way associative set for their cache. They decided to measure the time it took for a cache line to be re-cached after being removed from the cache. The idea is that you want to have long periods of time between re-caching, that way you do not waste time removing something from the cache that you are going to put back in soon. The results were analyzed qualitatively, rather than devising a quantitative metric to gauge the effectiveness of each strategy. 

I wasn't able to access the code on tera, so I pulled it from GitHub onto my account. The makefile also runs all of the simulations, so it is still running at the time of this writing.