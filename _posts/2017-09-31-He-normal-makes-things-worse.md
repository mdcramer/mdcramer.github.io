---
title: "He normal makes things worse"
excerpt: "I was disappointed when a fancy, modern initialization technique not only didn't help, but made things worse."
tags: [he normal, initializer]
last_modified_at: 2017-10-04
---

## Initializing weights is important
Initializing the weights properly can make the difference between a model that trains nicely and converges to a generalized solution and one that either explodes, never quite gets there or [trains more slowly](https://plus.google.com/+SoumithChintala/posts/RZfdrRQWL6u). The Udacity [sequence-to-sequency RNN example](https://github.com/mdcramer/deep-learning/tree/master/seq2seq) used a random uniform initialization (`tf.random_uniform_initializer(-0.1, 0.1, seed=2)`) for the encoder and decoder and then a truncated normal initialization (`tf.truncated_normal_initializer(mean-0.0, stddev=0.1)`) for the decoder dense layer, while [Weiss](https://medium.com/@majortal/deep-spelling-9ffef96a24f6) used a Gaussian initialization scaled by fan-in, also known as [He normal initialization](https://arxiv.org/abs/1502.01852).

Again, the training results were disappointing. Not only did the He normal initialization (achieved via `tf.contrib.layers.variance_scaling_initializer()`) not surpass the very basic random uniform initialization, but it performed worse. This is both disappointing and surprising, given that normal initializers typically surpass uniform ones.
<figure>
	<img src="{{ site.baseurl }}/assets/images/he-normal.png" alt="He normal initialization"/>
	<figcaption>Validation loss for various hyperparameter configurtations</figcaption>
</figure>
