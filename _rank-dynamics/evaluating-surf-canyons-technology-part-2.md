---
title: "Evaluating Dynamic Ranking Technology (Part 2)"
date: "2008-12-01"
tags: 
  - "top-posts"
  - "discovery"
  - "personalization"
  - "research"
  - "tutorials"
---

In a [Part I](/rank-dynamics/evaluating-surf-canyons-technology-part-1/), we began discussing some quantitative evaluations of the technology reported in our **[research paper](/assets/papers/SurfCanyonDemonstrationResearchPaper.pdf)**.  The goal in these studies is to see if search engine users get any value out of real-time implicit personalization and, if so, to find metrics that we can use to quantify this value.

One of the most useful techniques for comparing the quality of search engine retrieval functions is the technique of result interleaving, invented by [Thorsten Joachims](http://www.cs.cornell.edu/People/tj/) of Cornell University. He first introduced the idea in a [2002 paper](http://www.cs.cornell.edu/People/tj/publications/joachims_02b.pdf) and has since recently [expanded](http://www.cs.cornell.edu/People/tj/publications/radlinski_etal_08b.pdf) on the idea.

A search engine retrieval function is an algorithm that produces a ranked list of documents given a document collection and a user query. The retrieval function is the secret sauce behind the search engine. It is reported that Google, for instance, considers over 200 different document features when ranking web pages in response to a user query. These features are fed into the retrieval function which tells the web application which links to present and it what order.  In an open collection, such as the World Wide Web, different retrieval functions can produce both different document orderings as well as entirely different sets of documents.

Joachims came up with a very simple test that answers the following question: Given two retrieval functions, which does a search engine user prefer? His idea was that one can interleave the results of the two retrieval functions in an unbiased fashion and then count the user clicks on the links contributed by each retrieval function. The better retrieval function is the one that gets the most clicks.

For instance, assume that we have four documents (A, B, C, and D) that are relevant to a given query. According to the first retrieval function, r1, they should be ordered C-A-D-B. According to the second retrieval function, r2, they should be ordered D-A-C-B. The interleaved order of presentation would be D-C-A-B half the time and C-D-A-B half the time. We need to assure that each retrieval function gets to determine the document in the top spot half the time in order to have an unbiased test.  We would then show these document lists to many users as they conduct searches for this query. If we found that there were more user clicks on document C compared to document D, we can state that users prefer retrieval function r1. We can repeat this test for more documents and more queries, but by simply counting the clicks on documents contributed by each retrieval function we can determine an absolute user preference.

We implemented this test to compare our retrieval function, which employs real-time personalization based on implicit relevance feedback, with Google's retrieval function. We always show the user the top 10 Google results, even with our application installed, so our interleaving test was only done when users asked for a second page of search results. In those cases, the results presented to the user would be a mixture of results 11 through 15 from Google and the most highly ranked personalized results from our retrieval function.

The figure below shows the ratio of link clicks on dynamically ranked results compared to Google results as a function of the number of search results selected by the searcher before preceding to the second page of results. A ratio less than 1.0 would indicate that they prefer un-personalized Google results, whereas a ratio greater than 1.0 would indicate a preference for our retrieval algorithm. A ratio of 1.0 would indicate no user preference. Note that the users do not know if they are selecting personalized or un-personalized links. The result is a very clear preference for our retrieval algorithm – users are 30-40% more likely to select dynamically ranked links.

![Research Paper Fig 6](/assets/images/rank-dynamics/research-paper-fig-6.jpg)

We looked at this quantity versus the number of search results selected because the user's interactions with the search page are what we use to personalize the results. The more the user selects, the more confident we are about the user's true intent. Interestingly, users also prefer dynamically ranked results, by a significant margin, even when they skip the top 10 Google links entirely. When a user skips a link, we generally assume that the document is not what the user wanted. If the user skips all 10 links, we assume that the search engine misinterpreted the user intent and we start looking for different content that is not represented in the top 10 links.

Even though only 10% of searchers ever venture beyond page 1, we consider a 30-40% improvement in page 2 click-through rates to be significant. Quantitatively measuring the value delivered by real-time implicit personalization to page 1 results is, unfortunately, considerably more difficult. Nevertheless, be believe that these page 2 results are indicative of the value that real-time implicit personalization can delivery to page 1 results as well.

Update (7/15/09) - Our [research paper](/assets/papers/SurfCanyonDemonstrationResearchPaper.pdf), “Demonstration of Improved Search Result Relevancy Using Real-Time Implicit Relevance Feedback,” was selected for oral presentation at [SIGIR '09](/rank-dynamics/selected-for-oral-presentation-at-sigir-09/).

Update (12/18/09) - Our [research paper](/assets/papers/SurfCanyonDemonstrationResearchPaper.pdf) was published by [SIGIR](/rank-dynamics/selected-for-oral-presentation-at-sigir-09/).
