---
title: Motivation
excerpt: What is the motivation for this project?
tags:
- Perceptron
- motivation
last_modified_at: 2018-12-26 00:00:00 +0000
published: false

---
## Why build neural networks with a Perceptron class?

The obvious reason as to why neural networks are build using matrix math, as opposed to a Perceptron class, is simple: performance. Even if you're not using a GPU capable of massive parallel computations, the performance advantages of using matrices, to compute things like forward and backward propagation, are enormous. Having to go one neuron at a time while training, which is notoriously computationally intensive, could render the thing useless.

So why do it?