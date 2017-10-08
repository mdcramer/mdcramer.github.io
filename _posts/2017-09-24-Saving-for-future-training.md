---
title: "Saving for future training"
excerpt: "When training can last for days, and days, it's nice to be able to save the graph where it is an then pick it up again later."
tags: [training, saving, stack overflow]
last_modified_at: 2017-10-07
---

The Udacity [sequence to sequence project](https://github.com/mdcramer/deep-learning/tree/master/seq2seq) that I used as a starting point for the code actually had code to save and then reload the graph. I'm not sure why they decided to do that, but the graph is saved at the end of training and then reloaded right before it is used to make a prediction. So simply going back to continue training after the graph is saved should be easy, right?

Nothing is ever easy.

## Getting help from Stack Overflow
The problem was that while the Udacity project saved the graph, it only 'named' those variables necessary for the predictions. It did not 'name' those variables that are also necessary for continued training. This problem vexed me for days, so I finally went to [Stack Overflow](https://stackoverflow.com/questions/46374113/indexerror-when-loading-saved-tensorflow-graph-to-continue-training) for assistance. While there were a number of generous individuals who tried to give me a hand, in the end I had to figure it out myself. For the benefit of others who might stumble across the same problem, I went ahead and answered my own question.

## Setting up the script to run automatically.
While I was fiddling with the script I figured I would also get the thing to run 'automatically' from top to bottom. Part of the problem with Jupyter (or perhaps one of the benefits of Jupyter), is that you can manually execute the cells one at a time. When doing so it's easy to jump over any cells that shouldn't be run, for whatever reason.

Therefore, I arranged the code so that not only could it run from top to bottom automatically, but I could export the script to a .py file and run it from the command line. This will be handy for running in the background on EC2. Additionally, I added the ability to insert the command line switch "small" to indicate that the script should run on the small data. This turns out to be very handy for testing and debugging.