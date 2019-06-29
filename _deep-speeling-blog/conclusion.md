---
title: "Conclusion"
excerpt: "This was an amazing experience, but today I pulled the plug."
tags: [goals, conclusion]
date: 2018-10-06
last_modified_at: 2018-10-06
---

For a while there, thanks to taking the [Udacity Deep Learning Nanodegree](https://www.udacity.com/course/deep-learning-nanodegree--nd101), which is what got me hooked on deep learning in the first place, I had a bunch of free usage on AWS. A couple of months ago, however, my pool of free usage ran dry and, even though my instance has been dormant for a long time, I started getting charged ~$4 a month. Certainly not a lot of money, but I haven't worked on this project is almost a year, so I felt it was time to pull the plug.

Despite all my effort, in the end I was not able to reproduce the results on Tal Weiss' [Deep Spelling](https://machinelearnings.co/deep-spelling-9ffef96a24f6) blog post; he described getting 95.5% accuracy on the Validation set and I was never able to get much more than 75%. Apparently reproducing other people's results [can be challenging](http://blog.kaggle.com/2018/09/19/help-i-cant-reproduce-a-machine-learning-project). [Dong Wang](https://www.linkedin.com/in/wang-dong-69b8771a/), a software engineer who used to work at Pinterest, was able to develop a [spelling correction RNN](https://medium.com/@yaoyaowd/rnn-spelling-correction-to-crack-a-nut-with-a-sledgehammer-7f5aa442c08c) that reached 90% accuracy, but he was using a different data set.

The experience, however, was far from being a failure. Not only did I learn a ton from just banging the code together myself and then tweaking an running the models, it was actually a lot of fun. Every time I ran a model it was quite a thrill to watch the numbers come in and see what happened. If my energies weren't being devoted to a new job and other projects, I might be inclined to continue to push on this.

**Update: 17 October 2018** - In April 2018 The Atlantic published an interesting article about how the [Scientific Paper is Obsolete](https://www.theatlantic.com/science/archive/2018/04/the-scientific-paper-is-obsolete/556676/). In it, the author had this to say:

> "The more sophisticated science becomes, the harder it is to communicate results. Papers today are longer than ever and full of jargon and symbols. They depend on chains of computer programs that generate data, and clean up data, and plot data, and run statistical models on data. These programs tend to be both so sloppily written and so central to the results that it’s contributed to a replication crisis, or put another way, a failure of the paper to perform its most basic task: to report what you’ve actually discovered, clearly enough that someone else can discover it for themselves."

If the results in scientific papers are difficult to reproduce, it should be no surprise that blog posts on the internet would be even more difficult. For what it's worth, all of my code and data are available so should anyone who wishes to try to replicate my results encounter difficulty, please let me know.
