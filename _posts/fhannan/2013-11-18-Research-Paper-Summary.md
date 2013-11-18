---
layout: post
title: "Research Paper Summary"
description: ""
category: "blog"
tags: [blog, jekyll]
author: fhannan
---
{% include JB/setup %}


The paper is about compiling a program in memory in an “Instruction cache aware” way to minimize cache conflicts between procedures. The main issue is the conflicts between procedures on different threads (inter-thread account for an average of 21.21% of misses, usually due to the processor switching between threads often every cycle) than on the same thread (intra-thread accounts for an average of 20.47% of all misses, usually due to procedure calls). Inter-thread conflicts tend to not repeat with predictable patterns, making it more difficult to create optimization techniques. The program layout at the time of the paper made the problem worse. The paper also focuses on the direct-mapped caches that most frequently experience miss conflicts. 
The researchers looked at three situations to find potential solutions:

1)	Giving the compiler knowledge about programs that will be co-scheduled and control over the code. This usually applies for static workloads, pipelining or some communication mechanism, or when threads follow relatively different paths in the code

2)	Giving the compiler knowledge about programs likely to be co-scheduled and no control over the code of other programs. This uses the same scenarios but without remapping all the programs or when one application has several co-programs at different times. This is possible if there is run-time or load-time code modification to optimize program being run.

3)	Not giving the compiler this information at compile time. We can assume control over mapping logical pages to cache lines (physically-addressed cache is larger than system page size). Standard instruction cache layout optimizations make this assumption

If you are interested in a particular topic, the authors explain that the paper is split into the following sections: 

Section 2 – Background info on multithreading/instruction cache layout research

Section 4 – Methodology, what benchmarks they used, and how they measured results

Section 5 – Techniques for coordinated compilation of programs likely to be co-resident

Section 6 – Mechanisms for compiling one program given some knowledge of other programs likely to be run with

Section 7 –  How compiler and OS mechanisms reduce instruction cache misses even when the applications to be run together are not known

Section 8 – The techniques work for a range of cache associations and sizes

Section 9 – Conclusion

I looked at section 2 for past research on related topics:

Hwu and Chang worked on an algorithm to improve instruction cache performance with inlining (replacing function call site with body of what’s being called; risks larger size), basic block reordering (using a Weighted Call Graph and proximity heuristic), and procedure reordering compiler optimizations.

McFarling only cached frequently used instructions using a directed acyclic graph of procedures, loops, and conditionals. He tried to partition it so that each one was less than the size of the cache.

Pettis and Hansen used basic block reordering, procedure splitting, and procedure reordering to improve the code layout.

Hashemi et al computed which procedures occupy which lines. Torrellas et al mapped operating system code with an algorithm. 

Finally, Gloy and Smith used an algorithm called the Temporal Profile Conflict Modeling (TPCM). Information about procedure interleaving would go into a program trace. Kumar and Tullsen extend this to work for a multithreaded processor as it is based on temporal profile data and accurately models temporal the relevant cache mapping conflicts. TPCM can also be applied to code blocks of any granularity. 

In the last two sections, Kumar and Tullsen explain their results. They show how their techniques can be applied to other caches (associative caches and caches with different sizes) as well as what improvements they made for the three scenarios. When co-scheduling is expected, the best complication technique resulted in 11% performance improvement and around 20% with a remapping algorithm. They did not feel as successful with only co-scheduling predicted (one thread was accessible) as less results were given. When each program is mapped independently at compile time, the technique (with no remapping) achieved 13% performance time improvement for two threads and 27% for four threads.
