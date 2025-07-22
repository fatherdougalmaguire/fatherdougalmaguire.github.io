---
layout: post
title : "The building blocks of the Microbee"
tags:
 - Z80
 - Emulation
 - "Retro Computing"
 - MacOS
 - Swift
 - SwiftUI
 - Novato
toc: false
---
I'm approaching this project pretty much from ground zero ( both in terms of my knowledge of the internals of the Microbee and my skill as a coder ).  So most likely something you read here will be incomplete, non-optimal or completly wrong.  But it's a learning process and as I slowly forward with the emulator, expect a whole lotta refactoring and numerous mea culpas.

In the end though,  my stumblings should hopefully produce something worthwhile and I can look upon my journey with satisfaction.

#### The basics 

Notionally an emulator has a pretty simple structure.  It loops around and around,  executing instructions until it is stopped.

```swift
while emulator is running
{
    read next instruction from memory
    execute instruction
}
```

But the devil's in the details.  How can we expand this pseudo-code to define how a real Microbee would work ?

It's instructive to map out the components of the target Microbee model (32IC) for emulation.

- CPU : Z80A CPU running at 3.375Mhz
- RAM : 32Kb CMOS static memory ( battery backed up )
- RAM : 2Kb Video Display Unit (VDU) RAM
- RAM : 2Kb Programmable Character Graphic (PCG) RAM
- ROM : 4Kb Character ROM
- ROM : Microworld Basic
- ROM : Optional ( shipped with WordBee Word Processor or EDASM editor assembler )
- ROM : Telcom ( Terminal emulator )
- Storage :  Files and programs loaded and saved to audio casette.
- Video : Uses Synertek 6545 CRT controller. Monochrome output at 64\*16 characters or 80\*24 characters. 
- Sound : Internal speaker driven directly from the CPU.
- Keyboard : 60 key QWERTY layout.
- Serial port : An RS232-like serial port using a DB25 socket.
- Parallel port : 8 bit parallel I/O port via a DB15 socket.

At this point,  I'm not too fussed about emulating any I/O subsystems save video.  I chose to include video before other I/O as video output is memory mapped on the Microbee.  This means you can write to an area of memory and see the result.  This is probably putting the cart before the horse but it does provide visual feedback on how the emulator is proceeding.

So the immediate task will be to emulate the Z80 CPU, memory and video subsystems.

#### Z80

| Month    | Savings |
| -------- | ------- |
| January  | $250    |
| February | $80     |
| March    | $420    |

#### Memory

The Z80 has a 16 bit address bus.  So it can reference 2^16 or 65536 bytes ( or 64 Kb ) of memory.
For the Microbee 32IC,  memory is laid out as below :

|Address range|Contents|
|--------------|-------|
|0x0000-0x7FFF|User RAM|
|0x8000-0xBFFF|Basic in ROM|
|0xC000-0xDFFF|Optional ROM|
|0xE000-0xF000|Telcom ROM|
|0xF000-0xF7FF|VDU RAM|
|0xF800-0xFFFF|PCG RAM|
|0xF000-0xFFFF|Character ROM|

The interesting thing to note here is that the Character ROM address space partially overlaps the VDU address space.  
This is a concept known as *bank-switching*,  wherein different kinds of memory can be assigned to the same memory addresses and switched in and out when required. This was the only way to bypass the 64Kb limit.  Later models of Microbee implemented bank-switching to increase RAM to 512Kb and allow 64K of programs stored on ROM to be accessed.

In the following section,  we'll discuss what this means.

#### Video

Microbees used a Synertek 6545 display controller to output display information to CRT displays.  The 6545 

In the Microbee 32IC,  the display is memory mapped.  That is, each character position   

As noted previously, you can read from the Character ROM address space by setting the Z80's I/O port 11 to 1.
Writing to this address space will either write to VDU or PCG RAM.







 