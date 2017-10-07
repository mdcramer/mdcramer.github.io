---
title: "Motivation and Goals"
excerpt: "What is the motivation for this project and what are the goals?"
tags: [RNN, motivation, goals]
last_modified_at: 2017-10-04
---

## Using Deep Learning to correct spelling mistakes
### Motivation
This project was inspired by [Tal Weiss'](https://medium.com/@majortal) post on [Deep Spelling](https://medium.com/@majortal/deep-spelling-9ffef96a24f6). His [Deep Spell](https://github.com/MajorTal/DeepSpell/blob/master/keras_spell.py) code can be found on Github.

In January 2017 I began the [Udacity Deep Learning Foundation Nanodegree Program](https://www.udacity.com/course/deep-learning-nanodegree-foundation--nd101) and was hooked from the first lecture. I'd heard the term 'neural network' plenty of times previously, and had a general idea of what they could accomplish, but never had an understanding of how they 'work.' Since completing the course I've hadn't had much opportunity to tinker with the technology, but I've continued to contemplate it's uses, particularly in the domain of information retrieval, which is where I've spent the last decade focusing.

Unless you're Google, the typical technique for correcting spelling mistakes is the [Levenshtein distance](https://en.wikipedia.org/wiki/Levenshtein_distance), or it's close cousin, the [Damerau–Levenshtein distance](https://en.wikipedia.org/wiki/Damerau%E2%80%93Levenshtein_distance). Mr. Weiss does a good job of explaining why these do not work particularly well.

### Goals
* Re-implement Mr. Weiss' Recurrent Neural Network (RNN) using Tensorflow and achieve the same level of accuracy.
* Attempt to implement some of the areas for exploration he suggests, as well as others, to see if further improvements can be obtained.

### The beginning of the code
The first part of the code, which involves downloading the [billion word dataset](http://research.google.com/pubs/pub41880.html) that Google released and setting it up for training, is predominantly lifted from Mr. Weiss. The second part of the code, which involves building the graph and training the neural network, is borrowed from the Udacity [sequence-to-sequence RNN example](https://github.com/mdcramer/deep-learning/tree/master/seq2seq). This Udacity example works on a small dataset of 10,000 'sentences' (1- to 8-character words) and trains the network to sort the characters alphabetically. The current project contains code to handle both this large dataset as well as the small dataset, which is useful for debugging.
