---
layout: post
title: "Benchmark Research"
description: ""
category: "blog"
tags: [blog, jekyll]
author: fhannan
---
{% include JB/setup %}

(edit: I always forget the .md at the end of my post titles :-( )

This week's goal was to work with Eric and Paul to organize metrics to characterize the benchmarks we will use.

These are clarifications we established during the meeting and after emailing Professor Spjut:

- We do not want to compare simd and mimd or worry about that

- CUDA should run on either simd or mimd

- The metrics should be able to characterize instruction memory behavior of any given program for now

- The next step is to start characterizing certain benchmarks

The metrics I found:

- Low vs high cache intensity: I found categorizations called cache sensitivity and memory intensity, explained below (I think cache intensity is a term the paper Paul mentioned last week used in place of cache sensitivity; they sound like they should be the same thing).

- Cache sensitivity: use different cache sizes to measure how performance is affected. [This Carnegie Mellon University paper][paper1] used 1MB and 256KB caches to test performance degradation.
[paper1]: http://www.ece.cmu.edu/~safari/tr/tr-2012-003.pdf

- Memory intensity: misses per instruction (as opposed to overall miss rate). The same Carnegie Mellon University paper above tested this and ignored those with less than 1 for this metric (no misses per instruction) as the last level cache is not used. High memory intensity seemed to almost directly correspond to high cache sensitivity, but it is important to note that this is not always true.

- Instruction throughput: similar to average instruction read time mentioned in Eric’s post; the rate of instructions per second. We could do the rate of the instructions read.

- Harmonic speedup: I did not like this metric and I think we decided not to do it in a previous meeting (weighted speedup) but they compared speed for different programs with one benchmark; this particular paper (mentioned above) measured it for shared caches versus not shared.

- Branch misprediction: This could be the number of mispredicted branches, which lead to ineffective performance, and be done with a bimodal predictor. A bimodal predictor or saturating counter is a state machine with four states:

    - Strongly not taken
    - Weakly not taken
    - Weakly taken
    - Strongly taken

Some of these metrics came from [“Characterization of the EEMBC Benchmark Suite” by Jason Poovey, North Carolina State University][paper2]. This shows which metrics and categorizations they used to analyze the EEMBC Benchmark Suite, another potential benchmark suite for our project.
[paper2]: http://eembc.org/benchmark/characterization.pdf
