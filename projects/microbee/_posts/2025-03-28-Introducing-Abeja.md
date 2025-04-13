---
layout: post
title: "Introducing Abeja"
tags:
 - Z80
 - Emulation
 - "Retro Computing"
 - MacOS
 - Swift
 - SwiftUI
---

I only ever found a handful of emulators built for the Microbee and none were targeted at MacOS.

So I decided to roll my own

My implementation is called [Abeja](https://github.com/fatherdougalmaguire/Abeja "Abeja GitHub repository")  
Which is Spanish for **bee** ( a nod to my heritage ).

It is written for MacOS Sonoma ( v14.0+ ) using Swift/SwiftUI.

![Abeja](/assets/images/abeja-0.195.png)

Currently state of play : 

- It will attempt to start executing the BASIC interpreter in ROM
- It will show the contents of memory and registers during execution
- It show show a disassembly of the executing code
- You can step through executing code.
- A Metal shader is used to write output to the screen

However : 

- Only 1/3 of the Z80 instruction set is currently emulated.  So the CPU emulation quickly goes pear shaped
- No I/O functionality has been emulated. So there is no sound/keyboard/data storage as of yet.
- It's particularly slow.

Subsequent posts will document how to got to this point.

And the challenges in moving forward to a fully working implementation.





 