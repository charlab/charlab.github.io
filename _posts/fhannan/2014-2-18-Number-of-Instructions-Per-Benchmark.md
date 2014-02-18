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

Here is the parser code written in Python:


```cpp

def main() :
    file1 = './RAY/obj/x86_64/release/rayTracing.cu.o'
    file2 = './BFS/obj/x86_64/release/bfs.cu.o'
    file3 = './AES/obj/x86_64/release/rayTracing.cu.o'
    file4 = './CP/obj/x86_64/release/rayTracing.cu.o'
    file5 = './DG/obj/x86_64/release/rayTracing.cu.o'
    file6 = './LIB/obj/x86_64/release/rayTracing.cu.o'
    file7 = './LPS/obj/x86_64/release/rayTracing.cu.o'
    file8 = './MUM/obj/x86_64/release/rayTracing.cu.o'
    file9 = './NN/obj/x86_64/release/rayTracing.cu.o'
    file10 = './NQU/obj/x86_64/release/rayTracing.cu.o'
    fileNames = [file1, file2, file3,file4,file5,file6,file7,file8,file9,file10]
    #---------------------------------------------
    for fileName in fileNames:
    # Change this file name to load program 
    # whose instructions you want to count.
    #---------------------------------------------
            try:
        f = open(fileName, 'r')
            except: 
                break 

    #---------------------------------------------------
    # The start_str and end_str need to be added to each
    # .o file.
    start_str = '\t//start_file\n' 
    end_str = '\t//end_file\n'
    #----------------------------------------------------
    # exceptions is just a list of strings which helps us
    # recognize a legitimate CUDA instruction
    exceptions = ['.loc', 'file', '.param', '.entry', ';']
    
    lines_list = f.readlines()
    # take in the lines as strings and parse them into a
    # list by finding \n
    
    count = 0 # the count of the number of instructions
     

    for e in lines_list:
if e == start_str:
    count = 1    # This is a FLAG to start counting
if '//' not in e and (not(e == '\n')) and not(count == 0):
    for ex in exceptions:
        if ex in e:
            count += 1
        
if e == end_str and not (count == 0):
    break

    print "Number of instructions in %s: " % fileName,
            print count - 1

if __name__ == '__main__':
    main()
 
```


After running this code with the benchmarks we have, we got the following list of instructions per benchmark:



Name of Benchmark Program | Number of Instructions


AES - NA

BFS - 255

CP - NA

DG - NA

LIB - NA

LPS - NA

MUM - NA

NN - NA

NQU - NA

RAY - 2129



Note that NA means "not available." After looking at the code and number of lines for BFS and RAY, the number of instructions found for each, 255 and 2129 respectively, looks reasonable and close to the expected value.
