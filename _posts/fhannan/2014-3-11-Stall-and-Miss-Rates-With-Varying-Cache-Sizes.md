---
layout: post
title: "2014-2-25-Minutes"
description: ""
category: "sphynx"
tags: [blog]
author: fhannan
---
{% include JB/setup %}


I looked at the miss and stall rates of the benchmarks when varying the cache size. In particular, I looked at when there are three core clusters and the cache size changes from 2 to 4.

Here is a table of the data:

![datatable](http://i.imgur.com/Eec7yd9)


Here is a bar graph comparing the miss and stall rates for the 2 configurations for each benchmark. A data table is included underneath corresponding to each bar.

![comparisongraph](http://i.imgur.com/KPOrYjv.png)


The earlier benchmarks have significantly lower miss and stall rates than the lower one. Little difference is seen in comparison. The benchmark STO is hardly affected by this and RAY has a much higher stall rate (indicating more reservation fails than misses) than its miss rates, and is relatively very affected.
