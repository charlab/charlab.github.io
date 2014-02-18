---
layout: post
title: "2014-2-18-Number-of-Instructions-Per-Benchmark"
description: ""
category: "sphynx"
tags: [blog, jekyll]
author: fhannan
---
{% include JB/setup %}

At last week's meeting, we decided that we wanted to figure out the static number of instructions for each benchmark program. We did this so that we can have a better comparison and understanding of the benchmark programs. This is especially handy when we look at the stalls due to the instruction cache or instruction duplication, because we want to have the original and static numnber of instructions the program executes.

To do this, Akhil and I worked on analyzing and tweaking the benchmark programs, and making a parser to get the number of instructions.
                                                                     
                                                                     
First, we looked at the code for each program and what we wanted to use to parse it out. You can see this in the parser code included at the end of the post. Then, we added 


[still being edited]
