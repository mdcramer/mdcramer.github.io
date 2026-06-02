---
title: "Mo columns is mo better"
excerpt: "Getting and plugging in a Viewmaster 80-column card"
tags:
  - display
  - columns
date: 2026-06-01
last_modified_at: 2026-06-01
---

Developing on the Apple ]\[+ has been [very painful](/apple-2-blog/emulator#suffering-on-the-real-hardware). To alleviate some of that, I decided to get myself an 80-column card.

I have a strong recollection of having an 80-column card while in high school (I'm not sure how I could have used the machine otherwise), which was confirmed by one of my best friends, but for some reason there wasn't one in the ol' machine. (I still had my dot-matrix printer with the serial card but recently got rid of both. Not having a serial card is unfortunate. More on that later...) The good news is that for $80 plus tax and shipping (the kind gentleman threw in an extra cable and a couple jacks in case the old ones were too corroded) I was able to grab a Viewmaster [80-column card](https://en.wikipedia.org/wiki/Apple_80-Column_Text_Card) off [eBay](https://www.ebay.com/itm/198369480334?mkevt=1&mkpid=0&emsid=e11400.m144671.l197929&mkcid=7&ch=osgood&euid=d6474d7d5e2746ecb25ff351b1e89cfe&bu=43203910629&osub=-1%7E1&crd=20260527161229&segname=11400). This is most likely not the one I had in high school but that's fine. I'm getting used to the [disappointment](/apple-2-blog/hope) of not finding old stuff.

![Viewmaster 80-column card](/assets/images/apple2/80-column-card.jpg)

I plugged it in and, naturally, everything did not go smoothly. First, the connection was a bit strange. The Apple II+ was designed in 1979, long before 80-column text displays, so its motherboard is hardwired to output only a standard 40-column composite (with graphics) video signal from the RCA jack. When Applied Engineering built an 80-column card, they had to engineer around the fact the expansion slots could not send video data back to the motherboard’s video jack. Thus, I had to run the monitor OUT from the back of the machine into the box to connect with the TO COMP jack on the card. The second cable then goes from the TO CRT jack on the card out the back of the machine and into the monitor. Weird.

![Viewmaster 80-column card installed](/assets/images/apple2/80-column-card-installed.jpg)

Anyway, it works! Mostly. `PR#3` (the card is plugged into slot #3) turns on 80-column mode. Unfortunately, `PR#0` hangs the machine, so I have to CTRL-RESET. I don't remember anything like this from back in the day, but according to Gemini:

> The reason `PR#0` hangs your Apple ]\[+ is a known issue with DOS 3.3 / ProDOS and certain 80-column cards. When DOS intercepts the `PR#0` command it accidentally misdirects the computer's input/output vectors into an empty memory loop instead of cleanly passing control back to the motherboard.

Additionally, to get the screen to stop rolling I had to fiddle with the V.HOLD (vertical hold) and V.SIZE (vertical size) on the back of the monitor. Unfortunately, when switching back to 40 columns the screen starts rolling again. Finding settings that work for both 40 and 80 columns means giving up some vertical real estate on the screen. It's not a huge deal but since the analog signals are different, I had to find a compromise where the monitor's tubes successfully sync to both frequencies without the screen rolling or tearing.

<div class="image-grid">
  [![Writing code in 80 columns](/assets/images/apple2/ml-in-80-columns.jpg)](/assets/images/apple2/ml-in-80-columns.jpg)
  [![ProDOS in 80 columns](/assets/images/apple2/prodos-in-80-columns.jpg)](/assets/images/apple2/prodos-in-80-columns.jpg)
</div>

Also, apparently, I'm unable to have my program use graphics while having 4 rows of 80 columns of text at the bottom of the screen. That would have been cool, but while turning on HGR causes the Apple II+ to switch its internal video mode to graphics, the Viewmaster card does not know this happened because, as noted, its hardware disconnects the Apple ]\[+ motherboard's built-in video signal and generates its own independent 80-column text signal. The solution is, apparently, to turn off 80-column mode when running the program. Bummer.

So, at the end of the day, I could code in 80-column mode and then switch to 40-column mode when running the program. That being said, this is still a real pain. I can't believe I spent a zillion hours doing this in high school. Fortunately, there's a better way that keeps me out of the Apple ]\[+'s text editor entirely...