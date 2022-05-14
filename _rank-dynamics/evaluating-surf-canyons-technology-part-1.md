---
title: "Evaluating Dynamic Ranking Technology (Part 1)"
date: "2008-10-14"
tags: 
  - "discovery"
  - "personalization"
  - "research"
  - "tutorials"
---

For the past 2½ years, we have been working to improve the web search experience. In particular, we feel that search results individualized to each user and their current context will prove superior to search results that are not personalized to real-time intent. Our hypothesis is that real-time personalization works and the  challenge for us is to thus prove this statement, quantify the improvements and use the data that we gather to improve our application even further.

Quantifying the “web search experience” is, however, very challenging. Nevertheless, search engines are constantly running [small (and large) experiments](http://googleblog.blogspot.com/2008/08/search-experiments-large-and-small.html) to test how changes affect the user search experience. These experiments, which often use something called “A/B” or “bucket” testing, entail exposing a small, randomly selected set of users to the new features or changes and then comparing their behavior to the behavior of users on the baseline search site. Depending on the feature being tested, different user behavior signals are used to judge user satisfaction with the changes.

Since our technology radically changes the nature of the search results page, evaluating the application is particularly difficult. Once a user installs our browser application (Note: no longer available), the search engine results page becomes dynamic and personalized to each user. Users who install our application expect to get our technology, so a traditional bucket test is not possible. (If we were to have a control sample of users who installed a special version of our application that did not personalize their search results, those users would be perplexed and would probably uninstall the product.)

However, we performed a thorough evaluation of the technology using some traditional evaluation metrics from the Information Retrieval community as well as some new evaluation techniques that we invented ourselves. These evaluations are documented in a **[research paper](/assets/papers/SurfCanyonDemonstrationResearchPaper.pdf)** which we recently drafted. In a subsequent blog post, we will detail our evaluation methodologies and the conclusions of these studies.

A good presentation should naturally start with the conclusions, so we reveal here in advance the conclusion of our studies so far: real-time personalization works.

Update (12/1/08) - Continued in [Part 2](/rank-dynamics/evaluating-surf-canyons-technology-part-2/).

Update (7/15/09) - Our [research paper](/assets/papers/SurfCanyonDemonstrationResearchPaper.pdf), “Demonstration of Improved Search Result Relevancy Using Real-Time Implicit Relevance Feedback,” was selected for oral presentation at [SIGIR '09](/rank-dynamics/selected-for-oral-presentation-at-sigir-09/).

Update (12/18/09) - Our [research paper](/assets/papers/SurfCanyonDemonstrationResearchPaper.pdf) was published by [SIGIR](/rank-dynamics/selected-for-oral-presentation-at-sigir-09/).
