---
layout: post
title: "Introducing Abeja - the first iteration of a Microbee emulator"
tags:
 - Z80
 - Emulation
 - "Retro Computing"
 - MacOS
 - Swift
 - SwiftUI
 - Abeja
 - Novato
toc: false
---

Given that the Microbee range never sold in the same numbers as contemporary home computers such as the ZX Spectrum or Commodore 64,  there were only ever a handful of emulators built for the Microbee.  And these were primarily targeted at Windows and Linux platforms.

Since I use a Macintosh at home, I decided to roll my own.  And in a further act of bravado,  I attempted to do it completely scratch without studying any existing emulators.

This proved challenging on many fronts.

- The last time I had seriously coded was using Turbo Pascal on my early 90's PC ( I think it was a 386SX-25 ).  Swift was a whole new ballgame language wise.
- I had absolutely no idea how to code GUI apps.  
- I had only the vaguest clue about the hardware design and build of the Microbee.  

But I perservered and manage to knock out the first iteration, which I've named [Abeja](https://github.com/fatherdougalmaguire/Abeja "Abeja GitHub repository").  
For those that don't know Abeja is Spanish for **bee** ( a little nod to my heritage ).

![Abeja](/assets/images/abeja-0.195.png)

Abeja will run on Intel and Apple Silicon Macintoshes running MacOS Sonoma or later.

After much swearing and pulling of hair,  Abeja has gotten to the point that : 

- It will attempt to start executing the BASIC interpreter in ROM
- It will show the contents of memory and registers during execution
- It show show a disassembly of the executing code
- You can start/stop/pause and step through executing code.
- A Metal shader is used to write output to the screen

However the ahoc nature of Abeja's development has led to a less than optimal structure.

1) There is a lot of code for a barely functioning emulator.  
2) Only 1/3 of the Z80 instruction set is currently emulated.  
3) The hardware ( apart from the screen output ) is not emulated at all ( mainly because I have no idea how to capture keyboard input, interface with storage devices or enable audio output )  
4) Challenges with SwiftUI's [MVVM](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93viewmodel) framework results in major performance issues

So I'm going to take the ( many ) lessons learnt and start afresh.

[Novato](https://github.com/fatherdougalmaguire/novato) is the second attempt at the project.  
Novato is Spanish for **newbie** ( which is a terrible pun but also kind of apt ).



I'm going to use this blog to document the build of Novato step-by-step,  starting with first principles.




 