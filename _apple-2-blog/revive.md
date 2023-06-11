---
title: "Bringing the clunker back to life"
excerpt: "The old Apple ][+ had not been turned on in decades. It needed a lot of help to work again."
tags:
  - restoration
date: 2022-06-06
last_modified_at: 2022-07-03
---

All journeys start with a little inspiration. This one begins with a [series of Tweets](https://twitter.com/bzotto/status/1353797383201558531) from [@bzotto](https://twitter.com/bzotto). He tells a detailed story of how he restored, using custom hardware and software, and considerable gumption, a corrupted 5.25" floppy from elementary school. It contained a game that he wrote which he was able to salvage. I described [a game I wrote](https://mortalwayfare.com/in-the-beginning-there-was-basic/) in high school, along with [giving up ever seeing it again](https://mortalwayfare.com/remnant-from-the-past/). [@bzotto](https://twitter.com/bzotto), motivated me to embark on a quest to see if I could get my game back.

## Poof
I chronicled my [odyssey](https://twitter.com/markdcramer/status/1460289742726217733) on Twitter, but I'll share the highlights here.

After recovering the machine from my parent's house, where it spent decades in the closet and then the garage, I brought it back to San Francisco. I purchased a brand new set of [Apple DOS 3.3 floppies](https://www.ebluejay.com/ads/item/4249176), because I was skeptical that the old ones would still work, and was ready to see if it would boot. It turned on and did... something... but it did not look like it was working.

![The first boot in many, many years...](/assets/images/apple2/first-boot-with-fire-extinguisher.jpg)

After playing around with it a bit (swapping the floppy drives), I was able to get the BASIC prompt. I entered and ran a 1-line "HELLO WORLD", which worked. Then I smelled something awful and saw smoke coming out of the PSU. 

![PSC fries and gives off smoke](/assets/images/apple2/psu-goes-up-in-smoke.jpg)

Not having been powered on for decades, turns out a capacitor in the PSU dried out and fried.

## New capacitors
This is, apparently, a common occurrence with older power supplies. [@bzotto](https://twitter.com/bzotto), which whom I was chatting on Twitter, quickly identified the likely culprit (the 0.1 µf RIFA capacitor) and suggested a [replacement kit](https://console5.com/store/apple-2-power-supply-cap-kit-p-n-605-5703-astec-aa11040b-aa11040-b.html). Amazingly, there is an online store that sells a bag a replacement capacitors for the Apple ][+ PSU. According to folks on [Applefritter](https://www.applefritter.com/comment/95703#comment-95703) (a forum for vintage Apple computer hobbyists), this sort of thing happens a lot.

![Fried RIFA capacitor](/assets/images/apple2/fried-rifa.jpg)

With a little advice from the friendly people at Console5.com, who sold me the replacement capacitors, and a ton of help from my best friend, who lent me the work desk in his garage, we rebuilt the PSU. My initial thought was to only replace the RIFA, but I figured, while we're in there we might as well just change them all.

![Rebuilt PSU](/assets/images/apple2/old-vs-new-psu.png)

It was painstaking work that took many hours, and a steady hand, but in the end it was ready to go: the PSU, that is. The rest of the machine was still having a problem. When I booted the machine I got all kinds of strange things on the screen. Most frequently, however, were random green squares.

![Random green squares on the screen](/assets/images/apple2/green-squares.jpg)

## New RAM chips
The new suspect was the RAM. Another helpful person on Applefritter gave me some [code to test the RAM](https://www.applefritter.com/comment/95954#comment-95954), but after carefully typing it in I wasn't able to get it to work. Someone else suggested that I buy some contact cleaner and reseat all of the RAM chips, so I gave that a go. I bought the cleaner along with some chip removers and a multimeter. The good news is that every chip on the motherboard is in a socket, as opposed to being soldered to the PCB.

![Contact cleaner, chip removers and multimeter](/assets/images/apple2/cleaner-multimeter.jpg)

The process was slow and painstaking, but I eventually went through almost every chip on the motherboard. (There were a few under the keyboard that I wasn't able to reach without removing the motherboard.) The result, however, was disappointing; green boxes were still there. I read on forum that all the rows of chips were not required for the machine to operate, so I took some advice and tried with just a single row of RAM. The machine looked go, so after adding back the floppy drive I was able to get it to boot!

![Booting DOS with a single row of RAM](/assets/images/apple2/boot-with-one-row-ram.jpg)

This exercise clearly indicated that the problem was somewhere with the RAM. Taking a closer look at the pins, many of them were obviously corroded. So, I proceed to remove them, again, and gently file away the corrosion with an emery board. This worked well...

![Cleaning RAM pins](/assets/images/apple2/cleaning-pins.jpg)

... right up until it didn't.

![Broken RAM pin](/assets/images/apple2/broken-pin.jpg)

I tried to repair the broken pins with a soldering iron, but the work was too difficult. Eventually I decided that the hassle here was too great. Following [more advice](https://www.applefritter.com/content/replacement-ram-chips-tms4116-20nl) from the forum, I went online and purchased a full set of 24 replacement [TMS4116-20NL](https://www.questcomp.com/part/4/tms4116-20nl/408290989) RAM chips for $100, including shipping. They arrived in no time, with shiny pins, and worked like a charm. The machine booted immediately with no problems and I was able to run software off the new floppies I had purchased.

![Booting with new RAM](/assets/images/apple2/boot-with-new-ram.jpg)

We have liftoff!

In the meantime, with the help of my [new Twitter friend]((https://twitter.com/bzotto)), I tried to recover the old game from high school. That did not go as well.