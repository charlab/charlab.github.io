---
layout: post
title: "Expanding on Spock"
description: ""
category: "spock"
tags: [spock, blog]
author: estorm
---
{% include JB/setup %}

Over break I spent more time familiarizing myself with the codebase for Spock. There are already traces of simulations for the NAS Parallel Computing Benchmarks on tera, so there is already a lot of data to work with. Unfortunately, tera only has about 200 GB of free space so it is not possible to store all of the data on tera simultaneously. As a result, I ran the simulations a few at a time and copied over the final plots to my computer before deleting the data. 

I was able to run full simulation for 13 programs with 6 different cache configurations. 

The next step is going to be to try to create a method of more easily comparing data sets to pull out trends. The tentative plan moving forward is to use a web-based visualizer to easily compare the plots as well as make the information easily accessible. 

From a preliminary look, I found a jQuery plotter (http://www.flotcharts.org/flot/examples/) which may be suitable for interactively viewing the data. 