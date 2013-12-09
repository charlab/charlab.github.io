---
layout: post
title: "Starting Spock"
description: ""
category: "spock"
tags: [spock, blog]
author: estorm
---
{% include JB/setup %}

I spend most of this week familiarizing myself with the concept and implementation of the project. I read over the paper that was submitted as well as the reviews of the paper. In general the paper is lacking in thoroughness as well as any useful conclusions. 

I don't currently have access to the spock folder on tera, so I pulled the repository from GitHub. I looked through the makefile and all of the code and have a rudimentary understanding of what the programs are doing (unfortunately, they are almost entirely uncommented). I was able to successfully run the make file and generate the plots shown in the paper. Unfortunately, the traces themselves are linked from the protected spock folder on tera, so I didn't look at them. 

I was able to access the folder on tera with Pin. My plan for next week is to figure out how to use Pin and re-create the sp_omp trace to make sure I am using it correctly. From there I'd like to generate TTR plots for more programs to get a better sense of the metric. 