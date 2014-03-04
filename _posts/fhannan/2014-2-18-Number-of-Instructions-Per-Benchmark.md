---
layout: post
title: "2014-2-18-Number-of-Instructions-Per-Benchmark"
description: ""
category: "sphynx"
tags: [blog]
author: fhannan
---
{% include JB/setup %}

At last week's meeting, we decided that we wanted to figure out the static number of instructions for each benchmark program. We did this so that we can have a better comparison and understanding of the benchmark programs. This is especially handy when we look at the stalls due to the instruction cache or instruction duplication, because we want to have the original and static numnber of instructions the program executes.

To do this, Akhil and I worked on analyzing and tweaking the benchmark programs, and making a parser to get the number of instructions.
                                                                     
                                                                     
First, we looked at the code for each program and what we wanted to use to parse it out. You can see this in the parser code included at the end of the post. Then, we added the following lines of code in each benchmark program at the beginning and end of the file and used them to start and end counting instructions with the parser like so:

```cpp
start_str = '\t//start_file\n' 
end_str = '\t//end_file\n'
```

The criteria for a line to be an instruction was that it was not a comment (no '//' in it) or a blank line (such as '\n'). Then we checked to see whether it was an instruction based on whether there was a semicolon in the line or it had any of the following: .loc, .file,  .param, and .entry . These were the only instructions that did not end with a semicolon.


After running this code with the benchmarks we have, we got the following list of instructions per benchmark:


Name of Benchmark Program | Number of Instructions

| Benchmark                     | Number of PTX Instructions         |
| ----------------------------- | :---: |
| RAY                           | 2129  |
| BFS                           | 255   |   
| CP                            | 117   |   
| LIB                           | 1396  |   
| LPS                           | 298   |
| MUM                           | NA    |
| NN                            | 454   |
| NQU                           | 245   |
| STO                           | 27    |
-------------------------------------------------------------


Note that NA means "not available." After looking at the code and number of lines for BFS and RAY, the number of instructions found for each, 255 and 2129 respectively, looks reasonable and close to the expected value.
