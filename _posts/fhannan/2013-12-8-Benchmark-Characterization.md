---
layout: post
title: "Benchmark Research"
description: ""
category: "blog"
tags: [blog, jekyll]
author: fhannan
---
{% include JB/setup %}

This week, Paul and I looked at the benchmark that we have been able to successfully run so far, the Coulombic Potential (CP) benchmark. We measured values for the metrics we deemed important at last week's meeting. Here are the benchmarks we looked at at last week's meeting, along with the number indicating importance from 1 to 10:

Instructions loaded per cycle - 5

Average instruction read time – 3

Stalls due to instruction cache – 10

Instruction Duplication – 8 (important but potentially difficult to measure)

Average time to recache – low; ignored for now (paper not published for good reason)

Cache sensitivity – low (should be easy to measure)

Memory intensity – low (data but may be useful when we look at our benchmarks)

Instruction throughput – inverse view of stalls due to instruction cache, but also important

Harmonic speedup – ignored for now

Branch misprediction – ignoring branch predictors for now; they could mess up or we could mess up


This narrows it down to two metrics: stalls due to the instruction cache and instruction duplication. We also considered instruction throughput, but were not sure which data to look at for this. We decided to leave it alone for this week, since it is essentially an inverse view of stalls due to the instruction cache.

To measure stalls due to the instruction cache, we summed up the number of misses and the miss rates for the L1 and L2 instruction caches. This assumes that there is a stall for every miss. As of now, we are not sure if this is a correct assumption to make.

For the L1 instruction cache, we have 1599 misses out of 2072127 accesses, or a 0.008 miss rate. For the L2 instruction cache, we have 2079 misses out of 9014 accesses, or a 0.2306 miss rate.


Next, we looked at the instruction duplication. This means that an instruction was called repeatedly and perhaps more than would be efficient. If so, it would be a call from the same set and in the case of a miss (again, we would have to check whether this is a valid assumption). Then we looked at which set in a bank had the most accesses yet lowest miss rate, as this would imply the lowest instruction duplication. Ideally, we would take these sets and compare it to sets in another benchmark to analyze the instruction duplication.

For the L1 instruction cache, we have one set that has both the most accesses of 796 and lowest miss rate of 0.220. For the L2 instruction, we again have one set with the highest accesses, 576, but a miss rate equal to that of every other set, 0.500. In the future, we may not have only one set that fits both criteria.

__


Finally, we have a couple questions:
-How would we measure instruction throughput? We only get latencies outputted, so which one would we use? (Or maybe we're not measuring isntruction throughput at all, since stalls due to instruction cache is sufficient.)
-Are the assumptions we made (that every miss indicates a stall [and no forwards or nonstalls] and that the total misses are at least proportional to the total number of duplicate instruction calls) valid?
- We came across the following in the benchmark simulation printout and were going to analyze it, but we realized we do not know what it means. What does it mean?

"Number of Memory Banks Accessed per Memory Operation per Warp (from 0):
0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        0        
Average # of Memory Banks Accessed per Memory Operation per Warp=nan

position of mrq chosen"
