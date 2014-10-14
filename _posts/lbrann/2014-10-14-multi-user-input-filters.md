---
layout: post
title: "Multi-User Input Filters"
author: lbrann
description: "Alternatives and justification for board choice"
category: "MUSE"
tags: [MUSE]
---
{% include JB/setup %}

The following is an investigation of the different potential methods for 
filtering user input on large scale multi-user platforms.

## Background

Twitch Plays Pokemon featured two different modes for processing user input. 
Initially it took into account every input it could, but as more players began 
to play, it became too chaotic to remain purposeful, so this mode became known
as anarchy. Democracy was introduced to allow forward progress in
certain parts of the game that required precise user input. It simply recorded
only the input with the highest number of votes over a given time interval. 
Users could input "anarchy" or "democracy" into the IRC to influence which
mode was currently active. Based on this, I examined how other modes
for considering multi-user input would affect the individual user input.

## Different Impulse Responses

Josef suggested representing a vote for an input being represented by
different functions. In anarchy mode, each input was essentially an 
instantaneous impulse, whereas in democracy it acted as a step function for a 
given time interval.

Since anarchy is a simple queue, there isn't much I can think of to do with
regard to having a different impulse filters. However, if we consider different
filters on the response from each vote, we can achieve some much more 
interesting aggregates for democracy. 

## Democracy with Weighting - Input as a Meta-game

The first two basic ways I thought of was to store usernames and weight each
input based on the time that the user has been active. If it was weighted
more heavily towards older users, it would encourage long viewership, but
could discourage new viewers from getting involved. If it was weighted towards
newer viewers, it would encourage new or transient viewers to remain involved,
but could discourage long viewership. This would require a lot more overhead
if a stream gets a lot of viewers, so it doesn't seem scalable.

Since user-based information doesn't seem scalable, I moved to solely
considering time. Instead of each vote counting as a simple step response,
there could be a different function acting as a filter. The interesting aspect 
of having different responses is that with different maxima, user behavior could
change in order to maximize the effect of their votes.

An oscillating filter would incline the user to figure out the function being
used, and input their command at the time in the interval that it would be
one. If it oscillated between 0 and 1, it would decrease the effect of spamming,
but it wouldn't make it more interesting. If the oscillating filter allowed 
negative values, it would discourage spamming, and encourage planning inputs for
both desired and undesired commands. I thought about a red-light-green-light
system where during the green-light, votes count as positive 1 and during the 
red-light it would count as negative 1. The phases could switch randomly, so
the users would have to pay attention when they're inputting their commands.

So I then considered weighting each input based on collective behavior 
across a certain time interval. Since democracy already considered total 
votes during a time period, I thought about breaking up each time interval into 
smaller time intervals, and then at the end of the total time interval, 
aggregate votes and consider them as input. For example, consider
having a 10 second time interval that is split up into 5 2 second time 
intervals. Depending on what happens in each of the 2-second time intervals,
a certain input is chosen at the end of the 10-second time interval.

One way to consider the subintervals is to only consider the command that
had the highest density of user input during a subinterval. This would 
encourage large-scale collaboration to concentrate user input to a certain 
subinterval. In addition, this mode could consider more votes, or higher 
densities in subintervals other than the one with the highest density, 
negatively against that command. This way would not just encourage, but require
localized concentrations of inputs on certain subintervals.

Another way to consider the subintervals is to do the complete opposite of
the above, and only allow the input that had the lowest density over a given
time interval. This would just encourage no inputs at all, so having a large
number of votes during the total time interval counting as a positive bias
would be necessary. Then the input with the most distributed, large number of 
votes would be considered. Alternatively, it could consider the difference 
between the lowest-density subinterval and the next lowest-density subinterval
as a metric. Meaning that users would want to input at high numbers but widely
dispersed across the larger time interval.

The problem with the subintervals method is that it could make inputting
desired commands more difficult, as there would be more possibility to 
negatively affect undesired inputs. Although, it seems like it would still be
fair game, it would just require more work for the users. Assuming the majority
of people want to input a helpful command, they would still be able to, but
they would also need to defend against other commands by voting at
inopportune times for other

All of these methods of filtering input could add another interesting layer to 
the mere act of inputting commands, but it could detract from the focus on the 
gameplay. This could keep repetitive RPGs like Pokemon interesting, or serve
as a primary draw to a game.



