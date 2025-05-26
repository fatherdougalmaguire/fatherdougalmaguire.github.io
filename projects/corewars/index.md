---
title: "CoreWars"
layout: category
include_search : true
excerpt: I first read about CoreWars in old back issues of Scientific American.
toc: false
---
I first read about CoreWars back when I was at university.
( I was avoiding studying for a physics exam by reading old back issues of Scientific American )
And I was hooked.

CoreWars pits two programs ( written in simplified programming language called RedCode ) against each other in a virtual machine ( called MARS or Memory Array Redcode Simulator )

![pMARS screenshot](/assets/images/pmarssdl.png "pMARS screenshot")
\
Photo credit : [Wikipedia](https://en.wikipedia.org/wiki/Corewars "Wikipedia")

#### Let the battle commence

Each program ( or warrior ) takes turn in executing their code in a circular memory space or *core* ( when you reach the end of the core,  executing wraps around to the start ).
The program that executes the NOP instruction is deemed the loser,

Redcode itself closely resembles assembly language.

The code below is a particularly famous Redcode warrior called an *Imp*

```redcode
MOV 0, 1
```
An Imp simply copies itself one instruction ahead in the virtual machine ( using relative addressing )
And when it gets to that instruction, it copies itself again.  And so on.

A more complex warrior is known as a *Dwarf*
 
```redcode
ADD #4, 3        
MOV 2, @2
JMP -2
DAT #0, #0
```

I won't delve into the details of a Dwarf but essentially it writes a NOP every 4 address spaces,  'bombing' the core and hopefully eliminating the opponent.

Within this framework, these programs need to rely on complex strategies to defeat their opponents.  

Further,  genetic programming can be used to evolve warriors without human intervention.

Again,  I found that there were a dearth of MacOS based MARS environments.
 
So I decided to roll my own as my second major project.

#### On the links

- [Wikipedia](https://en.wikipedia.org/wiki/Core_War "Wikipedia")
- [Core War - the Ultimate Programming Game](https://corewar.co.uk/ "Core War - the Ultimate Programming Game")


