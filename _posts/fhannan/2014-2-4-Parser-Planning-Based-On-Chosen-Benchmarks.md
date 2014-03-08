---
layout: post
title: "Parser Planning Based on Chosen Benchmarks"
description: ""
category: "blog"
tags: [blog, jekyll]
author: fhannan
---
{% include JB/setup %}
 
 
Since Paul is now working on a different project, Sami, the newest member, and I are working on taking the work we've done regarding benchmarks and using it to make a parser.

Most of our meeting included refreshing my memory and catching Sami up on everything. Sami also may have a parser in Python that we can base our parser off of. Essentially, we want to tweak it to parse out the values needed to calculate the metris for a benchmark program. Afterwards, I worked more on looking at minutes I took for the last meeting of last semester (on 12/8). They are included at the end of this blog post for reference.

I looked back on the two main metrics we chose to characterize the benchmarks and measure their performance: stalls due to the instruction cache and instruction duplication. From this, I saw what we wanted to parse from the output file generated after running a benchmark program (recall that we were only able to run the CP benchmark successfully at the time). To look at stalls, we should look at the number of misses (assume that each miss leads to a stall) and reservation fails.

As for, instruction duplication, we want to look at the number of time multiple threads take the same instruction (as opposed to one thread). This is essentially how often we want to use simd. We also want to look at when banks want the request.

This means that we must parse those parts of the output file. I heard that Akhil and Donghyeon were able to run more benchmarks so hopefully, we can gather more ideas looking at those outputs and discuss what we can parse out.

Finally, at our meeting, Sami and I talked about figuring out how to take in a specified chunk of the parser and then search through that, rather than take in the whole thing. We are going to work on finding ways to do this once we know what chunk we want.


Here are the minutes from the meeting on 12/8 that I referred to:


Stalls due to instruction cache:
- L2 may not have instructions, definitely a data cache
- Reservation fail = could not reserve a register, because all the blocks in the cache were full with pending miss or the miss status holding register (MSHR) was full
- Reservation fails could be caused by conflicts (threads could run out of blocks to miss on)
- Reservation fails are another cause of stalls

Instruction duplication:
- We want to track how often different threads track the same instruction, not how often the same thread tracks it; how often do threads in parallel use the same instruction (how often should we use simd). This is a bit harder to characterize because  we have to look at specific instructions versus the number of instructions taken by a thread, which is in fact in the output.

- Or banks may want same request, but we cannot feed to both (PROBLEM and we could try to measure this)

This fermi (GTX480) only has 15 turned on; uses 15 L1 data caches (and 12 L2 caches) (15 core processors used)

We need a benchmark with more use of parallelism and multiple threads; we want to try more advanced programs to publish a paper
This is the naïve thing and we can say the naïve thing ended up being the best thing in the end, but we should try more complicated things, too (simple design works effectively [preferably cool, not naïve])
We want one small shared cache (probably worse than 16 independent caches, but maybe not and maybe it’s oversized in some cases)
Spjut will try to bring in server w/ gpu and put on network

Answer to our 3rd question:
•	Warp is a thread; we issue two and send two instructions to be executed in lockstep

We found the instruction cache at the top of the code printout!

- gpgpu_cache:il1     4:128:4,L:R:f:N,A:2:32,4 # shader L1 instruction cache config {<nsets>:<bsize>:<assoc>,<rep>:<wr>:<alloc>:<wr_alloc>,<mshr>:<N>:<merge>,<mq>}

- GPU config is a 4-way set associative cache

- Erik is changing cache to 16 to make it smaller and see if we get more conflicts (the sm; we need more cores per sm); 

- you need more cores if they’re running slower;

- care more about power efficiency; want it to be smaller (Did a lot for kepler, especially mobile version of kepler)
4 = 72 cores, 5 = full sm/kepler sm  logan

- The link for Paul: http://archive.is/uYtpO (GPGPU-Sim manual, definition of reservation fail)
