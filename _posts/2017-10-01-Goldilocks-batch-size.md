---
title: "Goldilocks batch size"
excerpt: "Some batch sizes are too big and some are too small. It's important to find the one that is just right."
tags: [batch_size]
last_modified_at: 2017-10-04
---

## Batch size of 64 is too small
As we learned in a previous post, a [batch size of 256]({{ site.baseurl }}{% post_url 2017-09-16-Smaller-batches-and-Dropout %}) is too large. Since then I've been running with a batch size of 128 when I got to thinking, if 128 is better than 256 then perhaps 64 is even better than that.

It is not.

For whatever reason, training with a batch size of 64 progressed significantly slower than all of the training with a batch size of 128. It was so poor that I cut it off before even completing the first epoch. I'll be going back to 128 now because, apparently, that one is "just right."
<figure>
	<img src="{{ site.baseurl }}/assets/images/batch_size-64.png" alt="Batch size 64"/>
	<figcaption>Validation loss for various hyperparameter configurations</figcaption>
</figure>
