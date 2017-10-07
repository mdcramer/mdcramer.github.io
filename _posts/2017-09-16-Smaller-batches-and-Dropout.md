---
title: "Smaller batches and Dropout"
excerpt: "Decreasing the batch size improved performance and adding Dropout helped even more."
tags: [batch_size, dropout]
last_modified_at: 2017-10-07
---

## Batch size of 256 is too large
I used a batch size of 256 during my first crack at training the RNN and, as can be seen below, it crashed before completing the first epoch. I'm not sure how long it took to get to that point, but it was probably only a couple hour in.

## Adding Dropout
Not only did dropping the batch size down to 128 improve training performance (the validation loss came down more quickly), but the RNN was able to successfully train for 6 hours on my local machine. That being said, it's generally a good idea to use some for a [Regularization](https://en.wikipedia.org/wiki/Regularization_(mathematics)) to prevent over-fitting. The Udacity project didn't have any Regularization, so I added 30% [Dropout](https://en.wikipedia.org/wiki/Dropout_(neural_networks)). This had the happy effect of initially increasing the rate at which the validation loss dropped, but at the end of the epoch it was still about the same without dropout.

The spelling correction is also not working particularly well. As an example, "he had dated forI much of the past" becomes "Sou had teap for much to heads tap". There's obviously more work to be done.
<figure>
	<img src="{{ site.baseurl }}/assets/images/batch256-and-dropout.png" alt="256 batch size and 30% Dropout"/>
	<figcaption>Validation loss for various hyperparameter configurations</figcaption>
</figure>
