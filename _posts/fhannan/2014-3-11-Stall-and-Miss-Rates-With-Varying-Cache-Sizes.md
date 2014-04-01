---
layout: post
title: "GTX480 Stall and Miss Rates"
description: ""
category: "sphynx"
tags: [blog]
author: fhannan
---
{% include JB/setup %}

[edited/corrected version]

I looked at the miss and stall rates of the benchmark programs when varying the number of sets (called NumSet) and ran on the GTX480 machine. In particular, I looked at a Unicore (or one core cluster) with a 64 KB block size and 4-way set associativity. The NumSet was varied as 2, 4, 8, 16, and 60.

Here is a table of the miss and stall rate data:

![datatable](http://i.imgur.com/M0mLKWw.png)


Here is a bar graph for the original miss rates. Note that there is basically no variability between BFS and STO.

![missgraph](http://i.imgur.com/68G8BvH.png)

Here is a zoomed in version so that we can look at the lower miss rates:

![missgraphzoom](http://i.imgur.com/bQi17i0.png)

Here is a bar graph for the original stall rates.

![missgraph](http://imgur.com/sDByQVS.png)

Here is a zoomed in version so that we can look at the lower stall rates:

![missgraphzoom](http://imgur.com/udjkHci.png)

The earlier benchmarks have significantly lower miss and stall rates than the later ones. Little difference is seen in comparison. The benchmark STO is hardly affected by this and RAY has a much higher stall rate (indicating more reservation fails than misses) than its miss rates, and is relatively very affected.
