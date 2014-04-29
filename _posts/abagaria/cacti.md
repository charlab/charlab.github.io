---
layout: post
title: "cacti"
description: ""
category: "sphynx"
tags: [gpgpu, sphynx]
author: abagaria
---
{% include JB/setup %}

I have been working on setting up CACTI on charlab in order to get more reliable power consumption results than the
simulator used by GP-GPUSIM. The process of installing all the dependencies was slightly annoyinng, but now there 
is a working copy of CACTI 6.0 in the gpgpu-sim folder. It can be run to generate a report using standard compile and 
run instructions (make and then run).
