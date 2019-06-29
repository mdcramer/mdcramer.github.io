---
title: "Motivation"
excerpt: "Why build neural networks using a Perceptron class?"
tags:
  - Perceptron
  - motivation
date: 2018-12-26
last_modified_at: 2019-01-06T04:50:00.000+00:00
---

## Why build neural networks using a Perceptron class?

The obvious reason as to why neural networks are built using matrix math, as opposed to a Perceptron class using an object oriented language, is simple: performance. Even if you're not using a GPU capable of massive parallel computations, the performance advantages of using matrices, to compute things like forward and backward propagation, are enormous. Having to go one neuron at a time while training, which is notoriously computationally intensive, could render the thing useless.

So why do it?

I've always felt that to fundamentally understanding something it helps to break it down into it's smallest components and then look at how each one operates. In the case of a neural network, that's the node, and the most fundamental form of a node is the [Perceptron](https://en.wikipedia.org/wiki/Perceptron "Perceptron - Wikipedia").

Naturally, this would eliminate the possibility of using a library, such as TensorFlow, but so much the better since the learning process is enhanced even further when building something from scratch. Finding examples of networks built using a Perceptron class was not easy, which is not surprising given the argument above, but I eventually stumbled across [An Introduction to Python Machine Learning with Perceptrons](https://www.codementor.io/mcorr/an-introduction-to-python-machine-learning-with-perceptrons-k7pn85vfi) which offered some helpful guidance to get off the ground.

After a lot of fiddling around I got it to work, built a few simple networks to do some linear classification and simple logic functions and actually had a lot of fun along the way. While I didn't find anything revolutionary, for anyone getting started with neural networks, or for those wanting to take a step back and look at things a different way, I'll walk you through what I did.

## Outline

Roughly speaking, after building a simple Perceptron class and then expanding its capabilities as I move forward, here's what I'll present:

1. Single node point and line classifier
2. Single node point and line classifier with bias
3. Single node logical gates: AND & OR
4. Multi-node logical gate: XOR
5. Multi-node point and parabola classifier
