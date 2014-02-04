---
layout: post
title: "Linux Screen Tutorial for ssh"
description: "Basic tutorial on using screen to manage remote shells"
category: "tutorial"
tags: [tutorial, screen, linux, ssh]
author: jspjut
---
{% include JB/setup %}

Since the projects for this group are using linux machines through
remote connections, I thought it might be useful to give a brief
tutorial on a tool called *screen* that is available on Linux.
Screen can be used as a way to manage a shell connection and allow the
connection to persist through network problems allowing you to resume
work where you left off.
For instance, if you name a screen session `gpgpusim` when working
from your desktop at home, you can then connect to the same screen
session using that name on your laptop during a group meeting in the
engineering building.
You can also leave a long running script active and connect to it when
you feel like it at any time.
Screen has many more features than the ones I will cover in this post,
but I thought it might be useful to give a brief introduction.
If you want more information than I provide here, there is a lot more
information available on the internet.

The first thing to do when you log in for the first time to work on
something is to start a screen session.
I recommend the following command because it will start the session
with a name:

```sh
screen -S gpgpusim
```

This will create a screen session and give it the name "gpgpusim"
allowing you to refer to it by that name in the future.
If you accidentally started screen without the name, I believe you can
name your session with the following while screen is running:

```
Control-a A
```

This means to hold the *Control* key and press the 'a' key then to
press a capital 'A' (shift-a).
*Control-a* is the magic combination that starts essentially all
interactions with *screen*.
For example, you can create a new *window* (screen's term for a new
terminal within the session) by using `Control-a c` and you can switch
between the first 10 windows with `Control-a #` where # is a number
between 0 and 9 corresponding to the window you want to switch to.
When you want to leave a session running but log out of the ssh
connection, you can use the following to detatch the session:

```
Control-a d
```

When you want to reattach to a session that has previously been
detached, you can use the following command where `gpgpusim` is the
name of the session to reattach to:

```sh
screen -R gpgpusim
```

If you don't know whether the previous terminal detached, you can add
the `-d` option to force it to detach. 
Alternatively, you can have multiple terminal connected to the same
session by using the `-x` option instead of `-d -R`.
If you use the `-r` option instead, it will reatach to whichever
session you were last attached to instead of having to provide a
session name.

An advanced setting that some people may want to change is switching
the default `Control-a` behavior to something else.
To change it to `Control-z` you can use the following command:

```sh
echo "escape ^Zz" > ~/.screenrc
````

which can also be undone by editing your `~/.screenrc` file.

For more help on screen you can type `Control-a ?` within screen, or
you can type `man screen` for the manual page.
