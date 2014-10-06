---
layout: post
title: "Game controller development board"
author: rpiersall
description: "Alternatives and justification for board choice"
category: "jetson"
tags: [jetson, board, arduino, gamepad]
---
{% include JB/setup %}

This post also represents contributions from [Kirk Lau]({{ site.url }}/people.html#knlau).

The following is a response to a question from Josef about why the
Arduino Pro Micro is the best choice.

The core issue in using the pro mini is that - much like other boards
in the $10 range - it lacks usb communication. In order to communicate
with the board, as we really need to do to have a usb controller, we
need either a usb-to-serial converter or a microcontroller capable of
directly using the protocol. Although these $10 boards can afford the
processor chip, LEDs, resistors, and such, the usb-to-serial chips
cost about $15 alone. 
(Note that the [Adafruit Arduino Pro Trinket](http://www.adafruit.com/product/2000) and
[Arduino Fio](https://www.sparkfun.com/products/10116) have mini-usb
ports, but these are only capable of
uploading new sketches and powering the board, respectively. It's not
a two-way connection).

This leaves us with a few options for usb communication. 
We can buy $20 [FTDI cables](http://www.adafruit.com/products/70), 
which have the usb-to-serial chip embedded
inside. However, Kirk and I both used these in E11 and they're
unreliable, bulky, and fragile. 
We can buy $15 [FTDI boards](http://www.adafruit.com/products/284), 
but that's still fairly pricey, adds another board to deal with, and is still
bulky and a point of failure. We could use a board that has the FTDI
chip and the microcontroller both onboard, like the 
[Arduino Nano](http://www.mouser.com/ProductDetail/Gravitech/ARD-NANO30NP/?qs=Vxac6xGyzPlh7in3DWNTbQ%3D%3D&gclid=CKTBoI-rl8ECFVVsfgodoQYAzg), 
but these are a good $30 and difficult to find (not very popular).

Our best bet is using a board equipped with the ATmega32u4 chip. These
were released less than two years ago, and have a built-in usb
transceiver, eliminating the need for any serial communication
whatsoever. 
There's a $23 [Adafruit Pro Micro](http://www.adafruit.com/products/1315) that uses this, as well
as a $20 [Sparkfun Pro Micro](https://www.sparkfun.com/products/12640).

Yes, the pro micro is twice the price of the pro-mini, but when you
take into account the extra hardware we'd have to buy to allow
communication to the PC with other boards, it's actually the cheapest
option available. If you want six analog inputs, the Adafruit pro
Micro has plenty. If we only need four and want to allow students to
buy a cheap [ADC chip](https://www.sparkfun.com/products/8636) 
if they really need more analog signals, we can
save a couple bucks with the sparkfun version. 
