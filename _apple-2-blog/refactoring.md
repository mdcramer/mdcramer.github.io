---
title: "Refactoring"
excerpt: "Changing the BASIC code... after only one week."
tags:
  - machine learning
  - synthesizing data
  - refactoring
date: 2025-07-13
---

Well, that didn't take too long. When I think about when I was developing [Mortal Wayfare](https://mortalwayfare.com/){:target="_blank"}, I frequently recall the amount of time I spent refactoring. I spent hours just looking at the code, trying to figure out how to better represent what I was trying to accomplish which improving the organization. Some days I would do nothing but this. Having never been a professional software developer, I'm not sure to what extent this is normal, but I found the process to be very helpful.

I suppose there's a balance between planning out what you're going to do and just getting started. For my Applesoft BASIC ML program, I leaned toward the latter. As such, after the first pass I already decided to change it up. More specifically, the first thing I decided to do was, rather than have a different array for each class of data, move everything into a single array. The reason is that, during training, this will facilitate looping over all the data.

Quick note on line numbers: refactoring BASIC almost _always_ consists of changing line numbers. As such, this code is not going to match up with previous posts. Hopefully that won't be too confusing.

```bbcbasic
100 REM == HYPERPARAMETERS ==
110 KN = 2: REM # OF CLASSES
120 DIM KN%(KN - 1): REM # OF SAMPLES FROM EACH CLASS
130 KN%(0) = 100
140 KN%(1) = 50

150 REM -- GENERATORS --
160 REM -- CLASS - MU-X0, MU-X1, SIG-X0, SIG-X1, RHO --
170 DIM GE(KN - 1,4)

180 REM -- CLASS 0 --
190 GE(0,0) = 100: REM MU-X0
200 GE(0,1) = 50: REM MU-X1
210 GE(0,2) = 30: REM SIG-X0
220 GE(0,3) = 10: REM SIG-X1
230 GE(0,4) = 0.5: REM RHO
240 GE(0,5) = SQR(1 - GE(0,4) ^ 2)

250 REM -- CLASS 1 --
260 GE(1,0) = 200: REM MU-X0
270 GE(1,1) = 100: REM MU-X1
280 GE(1,2) = 50: REM SIG-X0
290 GE(1,3) = 25: REM SIG-X1
300 GE(1,4) = -0.5: REM RHO
310 GE(1,5) = SQR(1 - GE(1,4) ^ 2)
320 REM == END HYPERPARAMETERS ==
```
To make that happen, I start by moving all of my generator hyperparameters into a single array, `GE()()`, where the first axis is the class. The second axis contains, respectively, \\(u_{x_0}, u_{x_1}, \sigma_{x_0}, \sigma_{x_1}, \rho\\) and \\(\sqrt{1 - \rho^2}\\). The last element is purely for performance since this quantity will need to be frequently calculated. Upon further refection I could have used \\(\sqrt{1 - \rho^2} \sigma_{x_1}\\) but this is a small optimization for later.

```bbcbasic
330 NS = 0: REM TOTAL # SAMPLES
340 FOR I = 0 TO KN - 1
350     NS = NS + KN%(I)
360 NEXT

370 REM -- DATA TABLE --
380 REM -- # - X0, X1, Y-HAT, Y --
390 DIM DS%(NS - 1,3)
```
After counting up the total number of samples, I then create `DS%()()` which replaces `AX%()` and `BX%()`. The first axis is the sample, of which there are `NS` in total. The second axis is, respectively, \\(x_0, x_1, \hat{y}\\) and \\(y\\). \\(\hat{y}\\) is the label (i.e., the class) and \\(y\\) is the prediction, which we'll get to later. Having all the data in a single array will facilitate generating and training.

```bbcbasic
400 REM -- REMAINING SAMPLES COUNT
410 DIM RK%(KN - 1)
420 FOR I = 0 TO KN - 1
430     RK%(I) = KN%(I)
440 NEXT

450 REM == GENERATE SAMPLES ==
460 FOR I = 0 TO NS - 1
470     REM -- ADAPTIVE QUOTA SAMPLING --
480     REM -- PICK CLASS BASED ON REMAINING SAMPLES TO GENERATE --
490     P% = RND(1) * (NS - I)
500     CS = 0
510     J = 0
520     CS = CS + RK%(J)
530     K = J
540     J = J + 1
550     IF P% >= CS GOTO 520
560     RK%(K) = RK%(K) - 1
570     REM -- GENERATE RANDOM NORMAL VARIABLES Z0, Z1 --
580     GOSUB 1400
590     REM -- GENERATE SAMPLE FROM Z0, Z1 --
600     REM -- X0 = MU-X0 + SIG-X0 * Z0 --
610     X0% = GE(K,0) + GE(K,2) * Z0
620     REM -- X1 = MU-X1 + RHO * SIG-X1 * Z0 + SQR(1 - RHO^2) * SIG-X1 * Z1 --
630     X1% = GE(K,1) + GE(K,4) * GE(K,3) * Z0 + GE(K,5) * GE(K,3) * Z1
640     DS%(I,0) = X0%
650     DS%(I,1) = X1%
660     DS%(I,2) = K
670     PRINT I + 1; TAB(5); "SAMPLE "; KN%(K) - RK%(K);
680     PRINT TAB(16); "IN CLASS "; K;
690     PRINT " AT ("; X0%; ","; X1%; ")"
700     ON K + 1 GOSUB 1200,1300
710 NEXT
```
Since I'd like for my data to be randomly sampled, rather than scrambling them after the fact, I decided to use 'adaptive quota sampling' to generate them randomly, which ending up with the appropriate quantities. I could have simply taken the end proportion of each class and use that to create probabilities during generation but then there would be no guarantee then the final proportions would be correct.

So `RK%()` holds the remaining number of samples to be generated for each class. Lines 490 to 550 then produce a random number `P%` which is from 0 to the number of remaining samples to generate and then figures out which class this should be based on the remaining number of samples to be generated for each. The beauty of this is that the probably of generating a sample in each class will be a function of how many remaining samples need to be generated. It took a while to debug, but in the end this produces exactly the number of samples in each class as specified in the hyperparameters.

The code from lines 580 to 690 is the same as previously, however, the class-specific variables have been replaced by `GE()()`, as mentioned above. Also, I changed `X%` and `Y%` to `XO%` and `X1%` to avoid confusion and be more consistent with the \\(y = \theta^T x + b\\) literature.

Line 700 is nifty. I don't recall using `ON... GOSUB` in high school but it enables branching based on the argument. I use `K+1` since the first class is \\(0)\\ and a zero argument doesn't branch.

```bbcbasic
720 REM == COUNT SAMPLES OF EACH CLASS TO VERIFY RESULT ==
730 DIM CT%(KN - 1)
740 FOR I = 0 TO NS - 1
750     K = DS%(I,2)
760     CT%(K) = CT%(K) + 1
770 NEXT
780 PRINT "TOTAL SAMPLES FOR EACH CLASS:"
790 FOR I = 0 TO KN - 1
800     PRINT CT%(I); TAB(5); "SAMPLES IN CLASS "; I
810 NEXT
820 END
```
For debugging purposes, I added some code to count the number of samples in each class to make sure it matched the hyperparameters. In the end, I decided to leave it. The loop is actually a bit slow but it's only run once.
