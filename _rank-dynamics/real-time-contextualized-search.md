---
title: "Real-time Contextualized Search - It is What We Do"
date: "2014-03-07"
tags: 
  - "top-posts"
  - "contextualization"
  - "discovery"
  - "personalization"
  - "recommendations"
---

When doing something that has never been done before (as we do), it can be challenging to describe it using familiar terminology in a way that doesn't create confusion while still conveying the newness of the idea. Large companies are sometimes capable of creating new terminology that is then adopted by others, but this can be particularly difficult for small entities. As such, for the sake of clarity, we describe how we have referred to our technology over the years and how we have now settled on "real-time contextualized search."

When [Surf Canyon](http://www.surfcanyon.com "Surf Canyon") launched its ground-breaking technology for dynamically re-ordering search results in response real time behavioral signals, we called our product a "[Discovery Engine for Search](http://blog.surfcanyon.com/2008/02/19/surf-canyon-launches-discovery-engine-for-search/ "Surf Canyon Launches Discovery Engine for Search")". The technology was referred to as "real-time implicit personalization" or simply "real-time personalization." Unfortunately, this created a bit of confusion with some people in the search community:

- The term "real-time" is an often abused and misunderstood. Technically "[real-time computing](http://en.wikipedia.org/wiki/Real-time_computing "Real-time Computing")" refers to guaranteeing a response "within strict time constraints." More generally it is used to refer to a system that responds very quickly. "Quickly," however, is subject to interpretation which is why we then sometimes referred to our technology as "instant" or "immediate personalization."
- Additionally, the term "personalization" may also lead to misunderstanding. In information retrieval "personalization" generally refers to collecting data about an individual over an extended period of time in order to generate models of that particular person's _long-term_ preferences in order to then use those models to modestly adjust relevance scores for _future_ queries. Despite [efforts to clarify the distinction](http://blog.surfcanyon.com/2009/01/14/the-four-quadrants-of-personalization/ "The Four Quadrants of Personalization") with "real-time personalization" the term "personalization" can lead to premature interpretation.

In 2009 the team at Surf Canyon authored a paper entitled "[Demonstration of Improved Search Result Relevancy Using Real-Time Implicit Relevance Feedback](http://www.surfcanyon.com/SurfCanyonDemonstrationResearchPaper.pdf "Demonstration of Improved Search Result Relevancy Using Real-Time Implicit Relevance Feedback")." The paper was subsequently [published by SIGIR](http://blog.surfcanyon.com/2009/07/15/selected-for-oral-presentation-at-sigir-09/ "Selected for Oral Presentation at SIGIR '09") after Professor Thorsten Joachims at Cornell University [offered a glowing review](http://blog.surfcanyon.com/2009/11/10/surf-canyon-surpasses-one-million-queries-a-day/ "Surf Canyon Surpasses One Million Queries a Day"). "Real-time implicit relevance feedback" is a mouthful but seems to alleviate misconceptions caused by the term "personalization."

The next year, a team of researchers at Cornell, lead by Professor Joachims, published a paper called "[Dynamic Ranked Retrieval](http://blog.surfcanyon.com/2010/10/30/citation-in-cornell-university-ph-d-dissertation/ "Citation in Cornell University Dissertation")" which built upon our SIGIR research by running tests using labeled results to compute relevance metrics. The results were not real-world, but [they were very impressive](http://blog.surfcanyon.com/2013/08/29/video-of-dynamic-ranked-retrieval-presentation-at-wsdm-2011-in-hong-kong/ "Dynamic Ranked Retrieval at WSDM '11") and their paper was selected as one of the six best at WSDM 2011. We found "dynamic ranked retrieval" to be more punchy than "real-time implicit relevance feedback."

Nevertheless, while "dynamic ranked retrieval" has its appeal, a recent post in [Search Engine Watch](http://searchenginewatch.com/article/2329882/Why-Yahoo-Wants-to-Move-Into-Contextual-Search-and-How-it-Might-Work-For-Them "Why Yahoo Wants to Move Into Contextual Search and How it Might Work For Them") regarding Yahoo!'s interests in search offered this:

> Contextual search works by algorithmically trying to determine what you really mean to search for, such as picking up cues _from the immediate preceding searches_, and presenting results based on that. \[Emphasis added\]

Algorithmically determining user intent by observing user interactions ("cues") is what Surf Canyon has been doing [since the very beginning](http://blog.surfcanyon.com/2007/09/19/hold-the-pickles-hold-the-lettuce/ "Hold the Pickles Hold the Lettuce"). Our contextual search, however, is taken one large and very important step further - rather than waiting for subsequent searches in order to exploit user behavior signals, our technology _immediately_ re-orders the result set in response to every user action that imparts additional understanding of the at-the-moment intent. As such, we henceforth declare that we develop Real-time Contextual Search.
