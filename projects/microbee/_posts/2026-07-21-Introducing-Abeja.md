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

But there is nothing like a stretch goal.  So I perservered.  Over the course of twelve months ( on and off ) and a reasonable amount of swearing, gnashing of teeth and pulling of hair, I managed to knock out the first iteration, which I've named [Abeja](https://github.com/fatherdougalmaguire/Abeja "Abeja GitHub repository").   

For those that don't know, Abeja is Spanish for **bee** ( a little nod to my heritage ).

Looks pretty shmick, no ?

![Abeja](/assets/images/abeja-0.195.png)

Abeja will run on Intel and Apple Silicon Macintoshes running MacOS Sonoma or later.

Abeja has gotten to the point that : 

- It will attempt to start executing the BASIC interpreter in ROM ( many thanks to Ewan Wordsworth of [Microbee Technology](https://microbeetechnology.com.au) for permission to use and include this ROM in the emulator )
- About 1/3 of the Z80 instruction set is implemented.
- It will show the contents of memory and registers during execution.
- It show show a disassembly of the executing code.
- You can start/stop/pause and step through executing code.
- A Metal shader is used to write output to the screen.

All in all, it's a pretty good start from a very low baseline.

#### There is always a but

Pausing to reflect,  I came to the realisation that the nature of Abeja's development has been somewhat adhoc.  This is lack of planning ( and detailed knowledge of emulation ) has led to a less-than-optimal structure.  

Specifically there are a few things that became apparent.

##### Shaky foundations

The video output routines were written first

##### Pulling a swifty

My knowledge of Swift is fairly rudimentary.  

##### I do declare

SwiftUI is a declarative UI framework.  That is,  you define what the UI interface should look like and the framework will handle any updates.

Below is the standard *Hello World* app in SwiftUI    

```swift

Import SwiftUI

@main
struct HelloWorldApp: App {
    var body: some Scene {
        WindowGroup {
            ContentView()
        }
    }
}

struct ContentView: View {
    var body: some View {
        Text("Hello, World!")
            .padding()
            .font(.largeTitle)
    }
}
```

Constrast this with a imperative UI framework like AppKit.  Here,  you define exactly what the UI interface and how it handles updates. 

```swift

import Cocoa

@main
class AppDelegate: NSObject, NSApplicationDelegate {
    var window: NSWindow!

    func applicationDidFinishLaunching(_ notification: Notification) {
        let screenSize = NSScreen.main?.frame ?? NSRect(x: 0, y: 0, width: 800, height: 600)
        let windowSize = NSMakeRect(0, 0, 400, 200)
        let windowOrigin = NSMakeRect(
            (screenSize.width - windowSize.width) / 2,
            (screenSize.height - windowSize.height) / 2,
            windowSize.width,
            windowSize.height
        )

        window = NSWindow(
            contentRect: windowOrigin,
            styleMask: [.titled, .closable, .resizable],
            backing: .buffered,
            defer: false
        )
        window.title = "Hello AppKit"
        window.makeKeyAndOrderFront(nil)

        let label = NSTextField(labelWithString: "Hello, World!")
        label.font = NSFont.systemFont(ofSize: 24)
        label.sizeToFit()
        label.frame.origin = CGPoint(
            x: (window.contentView!.frame.width - label.frame.width) / 2,
            y: (window.contentView!.frame.height - label.frame.height) / 2
        )

        window.contentView?.addSubview(label)
    }
}
```

Patently,  the SwiftUI version is a lot cleaner.  But there is a snag here.
It's a lot slower, executing at roughly 0.013 MIPS ( on an M2 Mac mini ) vs 0.489 MIPS for a real Microbee.   

##### Very hardware

The hardware ( apart from the screen output ) is not emulated at all ( mainly because I have no idea how to capture keyboard input, interface with storage devices or enable audio output ) and integrate this into SwiftUI,  not to mention adding to performance issues.  

#### Novato or once more with feeling

So I'm going to take the ( many ) lessons learnt and start afresh.

[Novato](https://github.com/fatherdougalmaguire/novato) is the second attempt at the project.  
Novato is Spanish for **newbie** ( which is a terrible pun but also kind of apt ).

I'm going to use this blog to document the build of Novato step-by-step,  starting from first principles and trying to get the basics right.




 