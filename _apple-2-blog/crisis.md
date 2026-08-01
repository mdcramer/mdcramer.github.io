---
title: "Crisis averted... I think..."
excerpt: "I started getting intermittent crashes to the system monitor which looked like a hardware problem."
tags:
  - crash
  - hardware
  - 80-column card
date: 2026-07-29
last_modified_at: 2026-08-01
---

Feeling pretty happy with my new volume knob, I turned back to running ML on my <span class="no-break">Apple ]\[+</span>. Then... I started getting crashes to the system monitor.

<div class="image-grid" markdown="1">
  [![Split code running on Apple \]\[+ hardware](/assets/images/apple2/crash-one.jpg)](/assets/images/apple2/crash-one.jpg "Split code running on Apple ]\[+ hardware")
  [![More split code running on Apple \]\[+ hardware](/assets/images/apple2/crash-two.jpg)](/assets/images/apple2/crash-two.jpg "More split code running on Apple ]\[+ hardware")
</div>

_No es bueno_. These types of system crashes are typically indicative of hardware issues. I struggled with a considerable number of these while [reviving](/apple-2-blog/revive/) the ol' clunker and am not particularly interested in revisiting that. What could have triggered these new problems?

## Did `RND(1)` break something?

My first thought was a recent test I ran to see how long it would take for `RND(1)` to return a value of exactly zero. My interest was related to the `log(0)` [vulnerability](/apple-2-blog/splitting/#squashing-dem-bugs) that I fixed previously. Does `RND(1)` ever return exactly zero, which would cause `log(0)` to crash? I don't know but I ran it 10s of thousands of times and never got one.

Regardless, could the strain from running `RND(1)` in a tight loop cause something to overheat and perhaps break? It's possible that this kind of sustained access pushed a chip's local temperature up a few degrees and exposed a marginal connection or borderline component that's been sitting right at the edge of failing for years. It might also be worth noting that Applesoft's `RND()` is fully deterministic from a cold boot, so the fact the system was crashing at different places ruled out a fixed logic bug or hard stuck bit.

Thinking about debugging this caused me to get a bit depressed but I jumped into running some diagnostics.

## Running diagnostics

### RAM

I started with the RAM. My first stop was an <span class="no-break">Apple ]\[+</span> [monitor memory test](https://erikarn.github.io/apple-ii/memory_test.html){:target="_blank"} that I've seen before. After carefully entering the long string of strange characters into the system monitor, it ran and passed clean.

Not convinced, I found an [Apple II Dead Test Diagnostic](https://www.youtube.com/watch?v=60skMMOYuAw){:target="_blank"} video that described replacing one of the system ROMs which would then run the diagnostic upon booting. You can find "dead test ROMs" on eBay for $40 but if the machine boots there's an alternate method of [downloading](https://github.com/misterblack1/appleII_deadtest/releases){:target="_blank"} the diagnostic and running it off a floppy. Because the machine kept intermittently crashing to the system monitor, it took a few attempts for [ADTPro](/apple-2-blog/adtpro/) to get the floppy image over to the machine but the result was a clean pass. Yay!

[![Result of the Apple Dead Test RAM diagnostic](/assets/images/apple2/apple-dead-test.jpg "Result of the Apple Dead Test RAM diagnostic")](/assets/images/apple2/apple-dead-test.jpg "Result of the Apple Dead Test RAM diagnostic")

### ROM

While testing RAM is as simple as writing values and ensuring that you can read back the same thing, ROMs are a little more difficult. The <span class="no-break">Apple ]\[+</span> has [6 ROMs](https://www.apple2faq.com/apple2faq/verify-apple-ii-roms/){:target="_blank"} (`$D000`, `$D800`, `$E000`, `$E800`, `$F000` and `$F800`) and they all are permanently burned with particular values. Rather than exhaustively check them all, I eyeballed each of them and then confirmed that the first several bytes of `$D000` matched its [known values](https://6502disassembly.com/a2-rom/Applesoft.html){:target="_blank"}. I could have done a checksum but rather than spend a lot of time here, I felt relatively satisfied and decided to move on. I could always come back to this later.

### CPU

Testing the CPU is even trickier because finding intermittent errors would require all kinds of stress testing. There's a GitHub repo with a [6502 functional test](https://github.com/Klaus2m5/6502_65C02_functional_tests){:target="_blank"} but there isn't an obvious way to download and run it, so I decided to just re-seat the chip. It's a small thing and was easy to do. I removed the Synertek SY6502 with date code 8119 (week 19 of 1981), wiped the pins and sockets with [DeoxIT](https://caig.com/what-is-deoxit-how-to-use-it/){:target="_blank"} for good measure, and then carefully put it back.

<div class="image-grid" markdown="1">
  [![6502 on the motherboard](/assets/images/apple2/6502-cpu.png)](/assets/images/apple2/6502-cpu.png "6502 on the motherboard")
  [![6502 socket on the motherboard](/assets/images/apple2/6502-socket.png)](/assets/images/apple2/6502-socket.png "6502 socket on the motherboard")
  [![Extracted 6502 processor](/assets/images/apple2/6502.png)](/assets/images/apple2/6502.png "Extracted 6502 processor")
</div>

None of this resolved the issue so I decided to start eliminating things.

## Process of elimination

Since starting this little adventure, I have added two cards to the bus: my [memory expansion (aka language) card](/apple-2-blog/memory/) from high school and an [80-column card](/apple-2-blog/mo-columns/) that I purchased off eBay. Since [ADTPro](/apple-2-blog/adtpro/) enabled writing code on my laptop with Visual Studio, the 80-column functionality is not something that I'm ever going to use. So I removed it first.

To my surprise and delight, after closing the machine back up, the problem seems to have gone away. How could this be? According to Claude, "Every card on the bus shares the same power rails and the same address/data lines; a card with a going-bad decoupling cap or a weakening bus driver can sag or inject noise onto those shared lines, and that tends to show up specifically under sustained heavy bus activity — which is exactly the pattern you've been chasing." While `RND(1)` never touches the 80-column card, it's possible the sustained, heavy-duty load might have revealed a marginal component on the shared bus. So the unused 80-column card is out and, happily, my K-mean program is back to running without any issues.

[![K-means running to the end without any crashing](/assets/images/apple2/clean-k-means-run.jpg "K-means running to the end without any crashing")](/assets/images/apple2/clean-k-means-run.jpg "K-means running to the end without any crashing")

Crisis averted. Now, hopefully, I can get back to coding...

## Update from Vintage Computer Festival

Ugh.

[![K-means crashing at the Vintage Computer Festival](/assets/images/apple2/vcf-crash.jpg "K-means crashing at the Vintage Computer Festival")](/assets/images/apple2/vcf-crash.jpg "K-means crashing at the Vintage Computer Festival")

I guess it's not _solely_ the 80-column card. I have a booth at the [Vintage Computer Festival](https://vcfed.org/events/vintage-computer-festival-west/){:target="_blank"} (more on that later) and, for what it's worth, have been demonstrating the K-means algorithm for over 3 hours straight. When I popped the lid I could feel the heat coming off the chips and could smell the "old computer overheating" odor. While only slightly warm to the touch, apparently that's enough.

[![Opening the case at the Vintage Computer Festival to cool off the machine](/assets/images/apple2/vcf-open-case.jpg "Opening the case at the Vintage Computer Festival to cool off the machine")](/assets/images/apple2/vcf-open-case.jpg "Opening the case at the Vintage Computer Festival to cool off the machine")

The good news is that popping the lid to let the internals cool down did the trick... for now...