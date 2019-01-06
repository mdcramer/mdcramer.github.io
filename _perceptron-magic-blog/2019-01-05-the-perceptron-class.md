---
title: The Perceptron Class
excerpt: Provide description of a Perceptron and build the initial, basic Perceptron
  class.
tags:
- Perceptron
last_modified_at: 2019-01-05 20:50:00 -0800

---
## What is a Perceptron?

The node is the 'atomic' unit of a neural network and the [Perceptron](https://en.wikipedia.org/wiki/Perceptron "Wikipedia definition") is the most basic form a node. Wikipedia describes it as an 'algorithm,' but you can also think of it as an 'object' that accepts some inputs and produces an output. Neural networks may then be constructed by stringing Perceptrons together and potentially stacking layers of them on top of each other.

Walking through the diagram below, a Perceptron will accept any number (n, for example) of inputs,`X0 to Xn`, and product a single output, `y`. These inputs are, of course, numbers, although they may be arbitrarily large or small and include fractions. Each input is then multiplied by a weight, `W0 to Wn`. The summation of all the inputs multiplied by their weights is called the hypothesis, `h(X) = X0 * W0 + X1 * W1 + ... + Xn * Wn`. The hypothesis is thus a single number which is then sent through an activation function. There are many types of activation functions (we'll review some later), but the simplest is the "step": if the hypothesis is positive or zero our output is `1`, otherwise it is `0`.

![](/assets/images/perceptron-architecture.png "Perceptron Architecture")

So what's the point of this? We'll dig into that, but at a high level what we've got is a linear classifier that simply checks to see if our hypothesis is either positive or negative. The key here, which we'll explore through a process called "training," is to determine the 'right' weights to make the Perceptron appropriately classify the inputs. That's what makes the magic: finding the weights.

## The Perceptron Class