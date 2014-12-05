---
layout: post
title: "Sphynx Technical Report"
author: jspjut
description: ""
category: "sphynx"
tags: [sphynx, research, publication, tech report]
---
{% include JB/setup %}

The first publication has been submitted from the group and is now 
[available online](http://arxiv.org/abs/1412.1140).
This publication is from the group that worked on the 
[Sphynx](/project/sphynx.html) project during the 2013-2014 school year. 
To give you a taste of the publication, here is the abstract:

```
The Sphynx project was an exploratory study to discover what might be done to improve the heavy replication of in- structions in independent instruction caches for a massively parallel machine where a single program is executing across all of the cores. While a machine with only many cores (fewer than 50) might not have any issues replicating the instructions for each core, as we approach the era where thousands of cores can be placed on one chip, the overhead of instruction replication may become unacceptably large. We believe that a large amount of sharing should be possible when the ma- chine is configured for all of the threads to issue from the same set of instructions. We propose a technique that allows sharing an instruction cache among a number of independent processor cores to allow for inter-thread sharing and reuse of instruction memory. While we do not have test cases to demonstrate the potential magnitude of performance gains that could be achieved, the potential for sharing reduces the die area required for instruction storage on chip.
```