---
layout: post
title: "2014-3-4-Shared-Cache-Designs-and-Microarch-Papers"
description: ""
category: "sphynx"
tags: [blog]
author: fhannan
---
{% include JB/setup %}

This week, I worked on the independent assignment of research alternate shared cache designs and looking at past Microarch papers.

First, I looked at ["Design and performance of directory caches for scalable shared memory multiprocessors"][link1] by Michael, M.M. It listed some general ideas about shared instruction caches that are already known but are still interesting. I am including part of their abstract:

[link1]: http://ieeexplore.ieee.org/xpl/login.jsp?tp=&arnumber=744354&url=http%3A%2F%2Fieeexplore.ieee.org%2Fxpls%2Fabs_all.jsp%3Farnumber%3D744354

"Experimental results show that the directory cache size requirements grow sub-linearly with the increase in the application's data set size. The results also show the performance advantage of multi-entry directory cache lines, as a result of spatial locality and the absence of sharing of directories. The impact of the associativity of the directory caches on performance is less than that of the size and the line size. We also find a linear relation between the directory cache miss ratio and the coherence controller occupancy, and between both measures and the execution time of the applications."


Next, I looked at ["Exploring the Design Space for a Shared-Cache Multiprocessor"][link2] by Basem A. Nayfeh and Kunle Olukotun.

[link2]: http://www-hydra.stanford.edu/publications/ISCA94.pdf

The paper looks at 3 parallel applications: Barnes-Hut, MP3D, and Cholesk. The execution time, speedup, miss rates, etc. were measured as the cache size was varied from 4 to 512 KB and the processors per cluster were varied from 1 to 8. Overall, miss rates decreased, execution time decreased, and speedup increased as cache size and processors/cluster increased. However, this is still interesting to look at to find a balance that we can work with when we vary our cache size.

