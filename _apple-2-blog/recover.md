---
title: "Recovering the old game"
excerpt: "The quest to recover my game from high school ended in vain, but the process was delightful."
tags:
  - restoration
date: 2023-06-11
---

As mentioned in [Bringing the clunker back to life](/apple-2-blog/revive/), the original motivation was to resurrect a [game](https://mortalwayfare.com/in-the-beginning-there-was-basic/) that I wrote in high school. I was obsessed with the game [Ultima](https://en.wikipedia.org/wiki/Ultima_(series)), beginning with [The First Age of Darkness](https://en.wikipedia.org/wiki/Ultima_I:_The_First_Age_of_Darkness), and so spent countless hours developing my own version.

The game logic was written in BASIC but this was much too slow for the graphics. Therefore, I convinced my parents to drive me to a remote bookstore to pick up a book on Apple ][ assembly (there were not a lot of resources in those early days) and then taught myself how to develop assembly subroutines that could be called from BASIC. I had a 2D array which I used as a map and then moved [hand-crafted images](https://mortalwayfare.com/remnant-from-the-past/) directly to the graphics memory as the character moved around. This already difficult process was more complicated by the fact the computer's graphics memory was interleaved and the Apple CPU didn't have a multiply command. Fortunately, the book offered a routine that would accomplish this with bit shifting and addition.

To this day I'm pretty proud of this little piece of computer wizardry and would love to see it again.

Alas, this is not to be.

## Box of floppies

Buried in my parent's garage for decades, alongside the old Apple ][+, was a box of 5.25" floppy disks. Was my game still on one of them?

![A very old box of 5.25" floppy disks](/assets/images/apple2/box-of-floppies.jpg)

For some unknown reason, my high school brain decided to just number the floppies, as opposed to just writing the contents on the stickers. I used to have a sheet that listed the contents of each disk, but that is long gone. Additionally, judging by the enumeration, it looks like some of the floppies are missing. I vaguely recall taking some to college. Was the game on one of them? Perhaps.

## A glimmer of hope on Twitter

I don't recall how I came across [@bzotto](https://twitter.com/bzotto) Twitter thread about how he [resurrected his high school game](https://twitter.com/bzotto/status/1353797383201558531) by reconstructing the data from an old 5.25" floppy, but it renewed my hope. He purchased some [specialized hardware](https://twitter.com/bzotto/status/1353800316693606402) that move repeatedly moved the drive head back and forth by fractions of a track to try to pull off enough magnetic signal to reconstruct the data.

Turns out [@bzotto](https://twitter.com/bzotto) is a great guy and extremely generous with his time, so when I reached out with my story he offered to help.

## Coffee shop excavation

In February 2022 we met at a coffee shop near his home. I brought the box of floppies and he brought the hardware and his Mac laptop. We spent three hours chatting as we tried one floppy after another.

The floppies almost always started with a bunch of red squares. His software would make an initial pass to see what could be read, and typically that was not very much. The floppy had been sitting in a damp, cold garage for decades and most of the magnetic material had degenerated or fallen off. It did not help matters that I purchased inexpensive, single density floppies in high school, and then recorded on both the front and back. It worked fine back then, but I was clearly not thinking long term.

![A lot of red squares](/assets/images/apple2/a-lot-of-red-squares.jpg)

As we patiently allowed the hardware and software to do its magic, something incredible happened. The red squares became green! Not all of them, but enough for us to identify what, if anything, was on the floppy. We were primarily interested in the catalog which, if memory serves correctly, was on track 14. I had a few floppies that I used for personal development, so the catalog would enable us to find these.

![Some signs of life!](/assets/images/apple2/some-green-squares.jpg)

## Disappointment

Unfortunately, the old game floppy was not to be found. We were able to identify the contents of every floppy we tried, but it wasn't there. As they closed up the coffee shop there was still a handful of floppies remaining. [@bzotto](https://twitter.com/bzotto) graciously offered to check them out at home, but no luck. I had printouts of my code, but we never saved them. It's also disappointing that I never made a copy, but this is not how young people think. I'll have to be satisfied with just the memory of what I put together.

## What next?

Nevertheless, I now have a [functional Apple ][+](/apple-2-blog/revive/) computer sitting on my desk. I don't have much time to devote to tinkering with an ancient piece of hardware, but it would be cool to see if I could run some modern machine learning algorithms on it. I'll be giving that some thought and will see what I can do...