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

Given that the Microbee range never sold in the same numbers as contemporary home computers such as the ZX Spectrum or Commodore 64,  there were only ever a handful of emulators built for the Microbee.

Those I know of are :

- A browser implementation of a Microbee 32IC called [NanoWasp](http://nanowasp.org/) "NanoWasp"
- The gold standard of Microbee emulators is [uBee512](https://www.microbee-mspp.org/repository/ "uBee512") ( Follow the instructions to obtain access to the *public* repository )
- A DOS and Windows version called PicoMozzy.  Available from the [Microbee Programmers Discord server](https://discord.gg/FTe93hNw "Microbee Programmers Discord server")
- The retro-arcade emulator [Mame](https://www.mamedev.org/ "Mame") can be used as well ( although it was a bit hit and miss in terms of Microbee models supported ).

As mentioned before, I decided to roll my own.  And in a further act of bravado,  I attempted to do it completely from scratch without studying the source of existing emulators or getting an LLM to write the code for me. 

This proved challenging on many fronts.

- The last time I had seriously coded was using Turbo Pascal on my early 90's PC. ( which I think it was a 386SX-25 )
Swift was a whole new ballgame language wise.
- I had absolutely no idea how to code GUI apps.  
- I had only the vaguest clue about the hardware design and build of the Microbee.  
- I had only the vaguest clue about how to write an emulator.

#### 5 minutes later

But there is nothing like a stretch goal.  So I persevered.  Over the course of twelve months ( on and off ) and a reasonable amount of swearing, gnashing of teeth and pulling of hair, I managed to knock out the first iteration, which I've named [Abeja](https://github.com/fatherdougalmaguire/Abeja "Abeja GitHub repository").   

For those that don't know, Abeja is Spanish for **bee** ( otherwise I would have to think up some variation of bee-related pun ).

![Abeja](/assets/images/abeja-0.195.png)

Abeja will run on Intel and Apple Silicon Macintoshes running MacOS Sonoma or later.

Abeja has gotten to the point that : 

- It will attempt to start executing the BASIC interpreter in ROM ( many thanks to Ewan Wordsworth of [Microbee Technology](https://microbeetechnology.com.au) for permission to use and include this ROM in the emulator )
- About 1/3 of the Z80 instruction set is implemented.
- It will show the contents of memory and registers during execution.
- It show show a disassembly of the executing code.
- You can start/stop/pause and step through executing code.
- A Metal fragment shader is used to write output to the screen.

All in all, it's a pretty good start from a very low baseline.  
And it looks quite nice,  especially from someone without much of a design sensibility. 

#### There is always a but

Pausing to reflect,  I came to the realization that the nature of Abeja's development has been somewhat ad-hoc.  This is lack of planning ( coupled with a fairly low knowledge of the intricacies of emulation ) has led to a less-than-optimal structure.  

Specifically there are a few things that became apparent.

##### Shaky foundations

I started a little arse-backwards.  The video output routines were written before the Z80 emulation core was even started.  And even those concentrated on getting something to appear on the screen that looked familiar, rather than faithfully modelling ( at least from a functional viewpoint ) the Microbee video hardware.

Which is not to say the experience was wasted ( I taught myself how to write a fragment shader after all ).  But you don't put up the walls and the roof of a house without pouring a concrete slab first.

##### Pulling a swifty

My programming **paradigm** ( so to speak ) lies back in the Turbo Pascal days.   And things have moved on quite a bit since then.

Things like :

- Concurrency
- Memory safety
- Extensions
- Protocols 
- Generics

Which are all documented here ([The Swift Programming Language](https://docs.swift.org/swift-book/documentation/the-swift-programming-language "The Swift Programming Language")) in a much better manner than I could do.

But the upshot is that there is a lot of cool language functionality that I should be taking advantage of to make the code base cleaner and easier to manage.

##### I do declare

As mentioned before,  GUI coding is something I no clear idea how to do.  Which is why SwiftUI seemed so appealing.

SwiftUI is a declarative UI framework.  That is,  you define what the UI interface should look like and the framework will reflect any updates to the application data based on UI interaction.

Take the following code which will generate a random Father Ted quote every time you press a button.

This is the interface bit that fetches a quote based on a button press.

```swift
import SwiftUI

struct ContentView: View

{
    // Create an instance of QuoteGenerator
    @State private var quoteGenerator = QuoteGenerator()
    
    // State variable to hold the current quote
    @State private var currentQuote: String = ""
    
    // Function to fetch a new random quote from the generator
    func fetchRandomQuote() {
        currentQuote = quoteGenerator.getRandomQuote()
    }
    
    var body: some View
    {
        VStack(spacing: 20)
        {
            Text("Father Ted Quotes")
                .font(.largeTitle)
            
            Text(currentQuote)
            
            Button(action: fetchRandomQuote)
            {
                Text("Get a Quote")
            }
        }
        .frame(width: 500, height: 400)
    }
}

#Preview {
    ContentView()
}
``` 

And this is the bit that stores the quotes and returns a random one.

```swift
import Foundation

class QuoteGenerator {
    // Array of quotes from Father Ted
    private let quotes = [
        "May your sheep grow big and strong, and may all the boys become popes.",
        "I think this is the beginning of a beautiful friendship!",
        "The trouble with having an open mind is that people will insist on coming along and filling it up with their own stuff.",
        "Father Ted is going commando. It’s like when you’ve got one sock and no idea where your other one has gone.",
        "It's not the size of the gift, but the thought that counts... until Christmas morning, then it's all about the size of the gift.",
        "I'm sorry, I didn't mean to be rude. It's just that sometimes when you're a priest and you can't even get into heaven, it makes you question everything."
    ]
    
    // Function to fetch a random quote
    func getRandomQuote() -> String {
        let randomIndex = Int.random(in: 0..<quotes.count)
        return quotes[randomIndex]
    }
}
```
You'll probably notice something important here.  

There is no execution loop.  The button is pushed, a new quote is returned and the framework updates the display.

This would work for stepping through an emulator but isn't really useful for running code.

Abeja solved for this issue using something like called a **TimeLineView**.  This is a display object that fires on a given schedule and updates the display.  This allows a bundle of instructions to be executed during the schedule period and then display the result.  

The main problem lies in the speed.  An 8 core M2 Mac Mini is averaging 50 micro-seconds per instruction.  This is 10x slower than a real Microbee.  

Now I don't know if this is a limitation of SwiftUI and the TimeLineView functionality or the way that I have implemented it ( I suspect the latter ).
But it's an issue to be solved ( and hopefully without having to scrap using SwiftUI altogether)

#### Novato or once more with feeling

Taking into account everything discussed above, I'm going to take the ( many ) lessons learnt and start afresh rather than try to beat the existing code base into submission.

[Novato](https://github.com/fatherdougalmaguire/novato) is the second attempt at the project.  

And once again, I'm treading down a familiar naming path.  Novato is Spanish for **newbie** ( which is a terrible pun but also kind of apt ).

I'm going to use this blog to document the build of Novato step-by-step,  starting from first principles and trying to get the basics right.




 