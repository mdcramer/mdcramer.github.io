---
title: "Hope springs eternal"
excerpt: "One more attempt, this time with Greaseweazle, to find the game."
tags:
  - restoration
  - Greaseweazle
  - FluxEngine
date: 2025-07-03
---

My ~~stupid~~ marvelous [game](https://mortalwayfare.com/remnant-from-the-past/) from high school is almost assuredly lost to the sands of time. While the attempt to find the bits, let alone excavate them, buried in my old stash of 5¼” floppies was [valiant](https://mdcramer.github.io/apple-2-blog/recover/), we found naught. I don’t know what I did with the floppy but I most likely, for reasons I’ll never remember, took it to college (I didn’t take the Apple ][+ but I did have an [Apple IIc](https://en.wikipedia.org/wiki/Apple_IIc)) where who knows what might have happened to it? It was probably used as a beer coaster and then eventually sent to the bitbucket at the bottom of the circular file.

Resigned, I looked at my box of archaic floppies and contemplated throwing them into the trash… when a thought occurred to me: what about the backsides?

Virtually all of my floppies are single sided, but as a broke high school student I didn’t care. Using a hole punch to open a write-protect notch on the other side of the floppy, I almost always flipped them over and wrote on the backside. Is it possible that, for some reason, I backed up the game on the “side B” of one of these floppies? Sure, I guess anything is possible.

So, I kept them. Because I am ~~stubborn~~ an optimist!

## Another helping hand

A few months later, a good friend, [Răzvan Surdulescu](https://www.linkedin.com/in/surdules/) (Principal Software Engineer, Robotics at Google DeepMind), came over to dinner with his family. Being a vintage computer enthusiast himself, who enjoys watching [videos](https://www.youtube.com/@adriansdigitalbasement) about restoring computers (who doesn’t?), he was thrilled to see the Apple ][+ sitting on my office desk. When I gave him the whole blah blah about the high school computer game, while my wife rolled her eyes as she left the room, he suggested we try recovering it with [Greaseweazle](https://github.com/keirf/greaseweazle/wiki/Yann-Serra-Tutorial).

Greaseweazle is an open-source USB device and software that allows you to read and write data from various types of floppy disks, including those used by old Apple ][+s. It captures the raw flux transitions from the floppy, enabling it to handle a wide range of formats beyond what is typically supported by standard floppy disk controllers. To get it to work, however, we’d need some new hardware.

## New hardware

While Răzvan had the latest v4.1 Greaseweazle [hardware](https://github.com/keirf/greaseweazle/wiki/Greaseweazle-Models) at home, we’d need a standard [Shugart](https://en.wikipedia.org/wiki/Shugart_Associates) floppy drive (not an Apple ][+ floppy drive) to read floppies. This is because Greaseweazle uses the Shugart interface to access the raw flux transitions on the disk, rather than relying on the drive's built-in encoding and decoding. This allows it to read and write various disk formats, including those with custom encoding or copy protection.

No problem. A few eBay searches later, I purchased this Toshiba 5¼" 1.2Mb Internal Floppy Disk Drive ND-08DE for $76. There were different DOS formats for the Apple ][+, but this capacity is significantly greater than the whopping 140Kb with Apple DOS 3.3.

![The Toshiba 5.25" floppy drive](/assets/images/apple2/toshiba-floppy-drive.jpg)

The new drive would also require some new cables to hook it up. They were inexpensive. Răzvan already had a few of the necessary cables and very helpfully made sure that I bought all the right stuff.

![Molex 4 pin female to female connector](/assets/images/apple2/molex-4pin-ftof.jpeg)

![36" Universal 34-Pin Floppy Drive Ribbon Cable for 3.5" and/or 5.25" Drives](/assets/images/apple2/floppy-ribbon.jpeg)

The opportunity to give it a go arrived when we were invited to a dinner party at the Surdulescu’s. We plugged everything into Răzvan’s beefy homemade Windows desktop, grabbed a couple flutes of Champagne and got to work.

![The full rig with Greaseweazle](/assets/images/apple2/rig-with-greaseweazle.jpg)

## Problems with the backside

The first thing I noticed was how quickly Greaseweazle was able to read data off the floppies. Unlike the [Applesauce](https://applesaucefdc.com/) USB disk controller that needed to grind back and forth to find the data using an original Apple ][+ floppy drive, Greaseweazle was able to find the floppy catalog in a second. (We used [FluxEngine](https://cowlark.com/fluxengine/index.html), seen below, which is different from the command line utility that comes with the GreaseWeazle, to test the directory of files on the disk. If that didn’t work, it had an option to read the flux off the disk which involved grinding back and forth to try to locate data. We had to do that quite a few times.)

![FlexEngine on the monitor](/assets/images/apple2/greaseweazle-monitor.jpg)

While we were able to find quite a bit of data, including a few titles from [Beagle Bros](https://en.wikipedia.org/wiki/Beagle_Bros), it seems the Apple ][+ may have used different kinds of data encodings to lay the sectors on the disk. Even if Greaseweazle can read the magnetic flux, the actual semantics of the flux (what sector goes where and in what order) can be opaque and the FluxEngine software might not interpret them in the right way. This might require more investigation.

After checking a few disks to verify that we were getting the same results as the last time I gave this a go, we decided to flip one over and try the backside. Immediately, we noticed that it wasn’t going to work. To calibrate the rotational timing, Greaseweazle uses the photoelectric sensor on the Shugart floppy drive which receives a ‘pulse’ every time the [index hole](https://www.atarimagazines.com/compute/issue34/019_1_MASS_MEMORY_NOW_AND_IN_THE_FUTURE.php), near the center of the floppy, passes over an LED. When you flip the floppy over, however, the index hole cutout is now no longer over the LED and so the pulse can’t be read.

One solution was to cut another hole in the floppy case. Given the proximity to the center of the floppy, however, this risked damaging the media. We explored some software solutions but then eventually decided it would be easiest to rip open the floppy and then manually flip the media. I had never opened a floppy before, but it was a relatively easy process. The old plastic was brittle and frequently crumbled in my fingers, but we were able to make it work.

![Opening a floppy disk](/assets/images/apple2/open-floppy-disk.jpg)

![Looking at the floppy media](/assets/images/apple2/floppy-media.jpg)

## Disappointment redux

Unfortunately, the result was no different from my previous attempt: there was no game to be found. The process wasn’t relatively quick. We were able to rip open and flip the media on about half of the floppies. There are ~25 to go so perhaps we’ll get to those one day. And then I’ll just discard everything. In the meantime, hopefully I’ll have some time to get back to deep learning…

![Deep learning on the Apple 2+](/assets/images/apple2/deep-learning.jpg)