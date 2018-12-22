---
title: "Reducing the Validation and Test datasets"
excerpt: "Depending on the situation, using smaller Validation and Test datasets can leave more data for training, and reduce time spent computing accuracy, without any impact on determining accuracy."
tags: [validation, test, datasets]
last_modified_at: 2017-10-23
---

Before starting the process of training, it is common practice to first randomly select a portion of the data to set aside for testing after training is complete. Then it is common practice to randomly select a portion of the remaining data for validation during training. The percentages used to split the data will [generally](https://www.youtube.com/watch?v=oJzDsnPq4vU) be a function of the amount of data available and the complexity of the model.

Out of habit, I chose to slice off 10% of the data to set aside for the Test dataset. When analyzing accuracy after each epoch, however, I began to notice that the accuracy percentages converged on a relatively stable determination long before the I finished running the Test dataset (see below). This seemed like a watch of both data and time, given that it took ~30 minutes to run the Test dataset. After consulting my colleagues at [CrossValidated](https://stats.stackexchange.com/questions/304977/can-i-use-a-tiny-validation-set), I decided to drop the amount of data set aside for the Test dataset from 10% to 2%. (The same thing could conceivably be done with the Validation dataset used during training, but I've been using a single batch for that.)

The result: A little more data for training and a little less time spend computing accuracy after each epoch. Meh, but why not?

<figure>
    <img src="{{ site.baseurl }}/assets/images/test-accuracy.png" alt="Measurements of accuracy with Test dataset after each epoch of training"/><figcaption>Extensive evaluation of Test dataset does not appreciable improve the determination of accuracy after a certain point.</figcaption>
</figure>
