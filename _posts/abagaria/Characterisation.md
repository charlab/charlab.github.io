---
layout: post
title: "Characterisation"
description: ""
category: "sphynx"
tags: [gpgpu, sphynx]
author: abagaria
---
{% include JB/setup %}

BFS finds use in state space searching, graph partitioning, automatic theorem proving,
etc., and is one of the most used graph operation in practical graph algorithms. The BFS
problem is, given an undirected, unweighted graph G(V,E) and a source vertex S, find
the minimum number of edges needed to reach every vertex V in G from source vertex
S. The optimal sequential solution for this problem takes O(V +E) time.
CUDA implementation of BFS. We solve the BFS problem using level synchronization.
BFS traverses the graph in levels; once a level is visited it is not visited again. The
BFS frontier corresponds to all the nodes being processed at the current level. We do
not maintain a queue for each vertex during our BFS execution because it will incur
additional overheads of maintaining new array indices and changing the grid configuration
at every level of kernel execution. This slows down the speed of execution on the
CUDA model.
For our implementation we give one thread to every vertex. Two boolean arrays,
frontier and visited, Fa and Xa respectively, of size |V| are created which store the BFS
frontier and the visited vertices. Another integer array, cost, Ca, stores the minimal
number of edges of each vertex from the source vertex S. In each iteration, each vertex
looks at its entry in the frontier array Fa. If true, it fetches its cost from the cost array
Ca and updates all the costs of its neighbors if more than its own cost plus one using
the edge list Ea. The vertex removes its own entry from the frontier array Fa and adds
to the visited array Xa. It also adds its neighbors to the frontier array if the neighbor is
not already visited. This process is repeated until the frontier is empty. This algorithm
needs iterations of order of the diameter of the graph G(V,E) in the worst case.
Algorithm 1 runs on the CPU while algorithm 2 runs on the 8800 GTX GPU. The
while loop in line 5 of Algorithm 1 terminates when all the levels of the graph are traversed
and frontier array is empty

Algorithm 1. CUDA BFS (Graph G(V,E), Source Vertex S)
1: Create vertex array Va from all vertices and edge Array Ea from all edges in G(V,E),
2: Create frontier array Fa, visited array Xa and cost array Ca of size V.
3: Initialize Fa, Xa to false and Ca to ∞
4: Fa[S] ←true, Ca[S]←0
5: while Fa not Empty do
6: for each vertex V in parallel do
7: Invoke CUDA BFS KERNEL(Va,Ea,Fa,Xa,Ca) on the grid.
8: end for
9: end while

AES
====

Given the flexibility of the memory model, it is possible to efficiently use the four T-lookup
tables each one containing 256 entries of 32 bits each. Unlike
previous GPU hardware, G80 is a scalar processor, so there is
no need to combine instructions in vector operations, in order to
get the full processing power. Furthermore, the native
availability of the 32 bit logical XOR operation on G80 speeds
up by orders of magnitude the execution of that fundamental
operation of the cryptographic theory. Thus, a single AES round
on a state can be done with 16 table look-ups and 16 32-bit
exclusive-or operations.
First of all, the input data and the expanded key are stored
in the GPU global memory space. As the final results show,
moving the data to and back from the device memory may
become the slowest operation when doing cryptography on the
GPU. It is due to the bandwidth of the PCExpress interface
which is only about 3,2 GB/s compared to the 50 GB/s of the
onboard memory of the GeForce 8800 graphics card. The precomputed
T-boxes are pre-loaded in the specific constant
memory of the device. The constant memory is cached and the
look-up table fully matches the size of the cache. The input data
is then divided in chunks of 1024 bytes which are encrypted or
decrypted completely in parallel. One CUDA block of threads is
responsible for computing one chunk of the input. The block is
composed of 256 GPU threads. An exhaustive research has
indicated that size to lead the fastest implementation. When
running the kernel code on the device, performance
improvement can be observed as the number of blocks
increases. So bigger input sizes lead to better performance.

Every GPU thread of the block computes four output bytes in
each AES round, so four threads encrypt/decrypt the whole
input state. Threads from the same block need to share and to
frequently access information of the AES expanded key. For
this reason it is loaded in shared memory together with the
portion of input processed by that block. More precisely, two
arrays of 1KB shared memory are used for the input, reading
data from the first and saving results of each AES round to the
second one. Then the arrays are swapped for the successive
round. This strategy allows to complete the encryption of the
input chunk without exiting the kernel. So it is done without
using the CPU to manage an external for loop to launch
sequentially all the AES rounds. At the end of the computation,
the resulted output data is written again in the global device
memory and then returned to the CPU.

CP
=====

Computes the short-range component of Coulombic potential at each
grid point over a 3D grid containing point charges representing an 
explicit-water biomolecular model.

MMU
====

 MUMmerGPU builds multiple suffix trees of the reference and
 partitions the query sequences into sets, called QueryBlocks, depending
 on the memory available on the GPU. Sequences within a given QueryBlock
 are aligned in parallel on the GPU.
 
 The algotithm used in MMU is shown here:
 
 http://www.biomedcentral.com/1471-2105/8/474/figure/F4
