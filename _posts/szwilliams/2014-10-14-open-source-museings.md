---
layout: post
title: "Open Source MUSEings"
author: szwilliams
description: "Journey through open source Twitch Plays Pokemon clones"
category: "MUSE"
tags: [MUSE, open source, IRC, game control, broadcast, stream, OBS, Tornado]
---
{% include JB/setup %}


##Existing Open Source Implementations

We decided to start our research into MUSE gaming by looking into open source implementations.
As MUSE was not much of a thing before Twitch Plays Pokemon (TPP) was created this past spring, every 
single open source MUSE gaming implementation we found was billed as a TPP clone, 
and written in Python. The open source 
projects referenced most often around the Internet when searching for TPP clones were:

* [`HeadlessCrowdEmulator`](https://github.com/strich/HeadlessCrowdEmulator)
* [`twitch-plays`](https://github.com/aidraj/twitch-plays)
* [`TwitchPlaysPokemon`](https://github.com/sunshinekitty/TwitchPlaysPokemon) (not the original)

After reviewing these projects, we realized that we would not be able to use any of them 
"straight out of the box" as each was designed to work with systems we did not have 
convenient access to (Windows and Ubuntu < 14), and certain aspects of the implementations 
would rely on system specific properties for key functionality (keypresses for Windows, 
X-windowing and streaming in Linux). In light of this, we identified the aspects of TPP that 
would have to be common to every project--interacting with the IRC chat, controlling 
the game, and broadcasting the game--and looked into how these aspects were implemented in 
each. 

### IRC Interaction
TPP is controlled by users inputting commands in the channel's 
chat window, which is connected to a dedicated IRC channel. Connection to and communication 
with an IRC channel using Python's built-in `socket` library is quite straightforward, and 
this approach was taken by two of the projects we looked into (`twitch-plays` and 
`TwitchPlaysPokemon`). In this approach, a connection is established with the IRC channel 
to a socket created with the `socket` library, and data is read from that socket and acted 
upon in a `while` loop. This simplicity in setup and interaction made dealing with IRC 
through the `socket` library a good starting design choice. The other implementation 
(`HeadlessCrowdEmulator`) 
connected to the IRC through Facebook's [Tornado](http://www.tornadoweb.org/en/stable/) web 
framework. This approached seemed very good in terms of scalability, but also was tied in 
with a lot of the main functionality and a custom GUI. Thus, Tornado appeared to be not the best 
starting design choice but certainly a possible path for future development (especially when 
considering how to deal with scaling).

### Game Control
Blackboxing the IRC connection and imagining we can grab commands as desired, we consider 
how those commands can be passed to a game. This proved to be the most system-specific 
aspect of TPP. Two of the implementations we looked at were made specifically for Windows, 
and the other specifically for "Linux" (though it seems it was made and tested only on 
Ubuntu 13 and Debian). The Windows implementations used the Python library `pywin32` for 
passing the keypresses to the game, and the Linux implementation used a combination of 
Python's `subprocess` library and [`xdotool`](http://www.semicomplete.com/projects/xdotool/). 
After further research into the subject, we found that passing keypresses to an arbitrary 
application can actually be rather annoying, and differs greatly between systems. So, 
we thought that the natural design decision coming from this was to write keypress passing 
software for the different systems specifically, while keeping the rest of the code as 
generalized as possible. For Windows, the `pywin32` library works as a good solution to passing 
keypresses to our game. For Mac OS X, a combination of Python's `subprocess` and AppleScript 
similarly allows for simple passing of keypresses. In Linux, we are not quite sure yet what 
will be used (the `xdotool` solution seems to rely a little to heavily on X Windows) but we 
are continuing to look into the matter.

### Live Broadcasting
[Twitch.tv](http://www.twitch.tv/) allows various methods of broadcasting live game footage 
from one's system. Front-line suggestions are GUI based broadcasting software such as 
[OBS](https://obsproject.com/), which provide a simple, reliable, and customizable setup of 
a live stream. However, most of this software is for Windows only (OBS just recently got an OS X 
version and a Linux version is in the works), which certainly restricts portability. This is 
the most system specific aspect of the whole project, and in many ways the aspect least connected 
to successfully building a MUSE implementation (there's nothing special about broadcasting MUSE, 
it's just like broadcasting any other game to Twitch). So, we decided that until further notice 
(or until OBS get to Linux), broadcasting the game to Twitch will be left to the user's volition, 
as this will most likely be easiest and best.

## Conclusions
Open source is awesome, but most of the projects we could find on this were quick things made 
last spring in the hype of TPP to work specifically with GameBoy emulators (mostly 
VisualBoyAdvance) on specific systems. In our desire to make a much more generalized framework 
for MUSE gaming, we found it best not to try and adapt one of these pre-existing implementations 
but rather to use these projects as guides. As the implementation of MUSE gaming is rather 
compartmentalized (connection/interaction, control, feedback), we can 
create a set of generalized and specified modules that can be mixed as necessary to work on 
many systems.








