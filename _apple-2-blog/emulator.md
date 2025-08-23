---
title: "No Cursor, no emulator"
excerpt: "While the modern tools are at my disposal, I am, for the most part, not using them."
tags:
  - Cursor
  - emulator
date: 2025-08-16
last_modified_at: 2025-08-23
---

A few weeks ago, after reading this [blog](/apple-2-blog/refactoring), a good friend sent an email with some interesting questions:

> Are you actually writing and running your code on the real physical Apple ]\[, or are you using an emulator? If you're using a real one, how are you transferring the code back and forth from the Apple ]\[ to the blog? I'm guessing you're not using generative AI to write the code, since it sounds like writing it by hand is part of the fun. Is that right?

I sent him the answers but I thought I might share here, too.

## Running on the real hardware

He might have missed my post about [bringing the clunker back to life](/apple-2-blog/revive) but I'm running on the real hardware from early '80s, which I recently refurbished with new capacitors in the power supply and new RAM chips on the motherboard.

I can't remember exactly when my parents ponied up a bought me the Apple ]\[+ but it was after years of me hassling them relentlessly. In their defense, no one had a personal computer back then and it wasn't entirely clear what one would do with one. The machine was _very_ expensive and they didn't want to pay that kind of money for a video game machine. I vaguely recall the Apple ]\[+ with a pair of floppy drives costing ~$2000 plus a few hundred for the extra 16k RAM on the expansion memory card and ~$500 for the dot matrix printer. That would be ~$9000 today. (For comparison, we had a [Magnavox Odyssey<sup>2</sup>](https://www.youtube.com/watch?v=DYVH2IHnH8U&t=300s){:target="_blank"} which was under $200. The cartridges were ~$25.) My father was an aircraft mechanic and my mother stayed home to raise two children, so they paid close attention to finances.

My obsession with the Apple computer began during the summer after the 6<sup>th</sup> grade. My mother signed me up for computer camp where we learned how to write code on the Apple ]\[. These machines didn't even have floppies, so we used cassette tape recorders. You'd press 'record' on the tape recorder before entering `SAVE` to store the program. To get it back you'd type `LOAD` and then press 'play' on the tape recorder. It wasn't punch cards but that's wild. My program was a lowres picture of a Star Wars battle (another childhood obsession).

From that moment, I had to have one. Every single birthday or holiday from that point forward, when anyone asked me what I wanted, to everyone's dismay, I'd say, "Money." My plan was to save up enough to get one. In the meantime, since these computers were not readily available, I would write BASIC programs on notebook paper (to do what, I can't remember), ride my bike to the mall and then try them out on the [TRS-80 Color Computer](https://en.wikipedia.org/wiki/TRS-80_Color_Computer){:target="_blank"}s at Radio Shack. As I recognized at the time, the sales people there were extremely cool to let me do that.

Saving up that kind of money took years but sometime around the 9<sup>th</sup> grade I had enough to get a TRS-80, which was significantly less expensive at about half the cost. My parents, realizing that I was about to drop every penny I had on a computer inferior to the one I really wanted, stepped up and surprised me. I can still remember the boxes sitting in the living room when I got home.

## Suffering on the real hardware

While I know that there are [emulators](https://www.applefritter.com/content/apple-ii-online-emulator-0){:target="_blank"}, which would probably make life easier, I am not using them. While writing Applesoft BASIC on the original hardware feels _authentic_, it comes with some challenges:

* The keyboard works but it's 40+ years old and isn't particularly ergonomic.
* The monitor is only 40 characters wide because, for some reason, I don't have the [80-column card](https://en.wikipedia.org/wiki/Apple_80-Column_Text_Card){:target="_blank"}. (I vaguely recall having an 80-character wide display but perhaps that was on the school's computers. I also remember having a color monitor but that must have been the school as well.)
* Reading the code requires the `LIST` command but without specifying line numbers the entire program will quickly scroll by. Therefore, I have to painstakingly enter the line numbers each time.
* There isn't a particularly effective way to edit lines of text. This super enthusiastic dude [demonstrates](https://youtu.be/PHfKCxjsmos?si=LbrDEIzWVNBPsF8K&t=108) how to use the `ESC` character to edit a line of code but it's a real hassle. I've used this (although on my machine, which I found in the manual, you have to use a, b, c and d, which is confusing, plus hold down `ESC` the entire time) but it's almost always easier to just retype the line. (**Update**: The I, J, K, M works and `ESC` toggles if you use those keys. It takes a little getting used to but it's much better.)
* Applesoft BASIC has a "debug mode" with `TRACE`, which essentially prints out line numbers as they're executed, but I've never used it. It sounds like a nightmare.

## Transferring Applesoft BASIC code to this blog

While there's probably a way to connect the Apple ]\[+ to my Windows machine, I solve this problem by taking a picture of the monitor with my phone and then asking [chatGPT](https://chatgpt.com/share/684f9647-c438-8010-86d6-a3eae68a7b7d){:target="_blank"} to extract the code. The first attempts weren't too bad, but I had to iterate quite a few times to get it to output correctly. For example, if a single line of code wrapped on the screen, chatGPT would add extra line numbers. It also messed up the counting on occasion. It sometimes interpreted the percent sign as a dollar sign. That being said, it saves me a _ton_ of work. Interestingly, I think I 'trained' chatGPT on how to read the Applesoft BASIC code because outputs have become increasingly higher quality.

![First screenshot of code](/assets/images/apple2/code-pic-1.jpg) ![Second screenshot of code](/assets/images/apple2/code-pic-2.jpg) ![Third screenshot of code](/assets/images/apple2/code-pic-3.jpg)

I tried taking a video of the entire program scrolling by but the quality was not good enough for OCR.

## No generative AI

Or not much, at any rate. GenAI is amazing and Cursor is beyond fantastic, but, as my friend said, part of the fun is writing the code myself. I'll admit to getting assistance with [adpative quota sampling](/apple-2-blog/refactoring#generating-the-samples), which isn't particularly difficult. I've also asked about how some commands work (e.g. `RND()`) although I've been relying primarily on the original [reference manual](/apple-2-blog/synthesizing-data). The rest, however, is me.