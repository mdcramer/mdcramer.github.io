---
title: "Check out the guts"
excerpt: "Providing users a representation of what is happening in the bowels of the personalization engine."
date: 2026-11-11
last_modified_at:
tags: [patent, sidebar]
---

I did something with the prototype which some folks might find curious: creating a left nav bar with information about what sorts of things are being stored in memory, how they are clustered and what weights are being assigned to them.

[![Screenshot of memories sidebar on MyMemoChat](/assets/images/llm-personalization/memories-sidebar.jpg "Screenshot of memories sidebar on MyMemoChat")](/assets/images/llm-personalization/memories-sidebar.jpg "Screenshot of memories sidebar on MyMemoChat")

It's highly unusual for a ranking, personalization or other ML system to expose intricate details around operation of the underlying engine, but I do it here for instructive purposes. I would not recommend that such a thing be put into production, but it is helpful when building and debugging a prototype.

## Patent: Adaptive user interface for real-time search relevance feedback

This idea is not new for me. In the very early stages of building [Rank Dynamics](link to blog), I did something very similar. Sadly, I did not save a screenshot of the early prototype, however, I drew up what we built in my patent, [Adaptive user interface for real-time search relevance feedback](https://patents.google.com/patent/US8117197B1/en){:target="_blank"}.

[![Fig 5 from patent US20070260597A1](/assets/images/llm-personalization/US20070260597A1-Fig5.png "Fig 5 from patent US20070260597A1")](/assets/images/llm-personalization/US20070260597A1-Fig5.png "Fig 5 from patent US20070260597A1")

The 'primary' keywords come from the user's query while the 'subordinate' keywords are implicitly pulled from the search context by observing user behavior. When I user selects a result, we would extract the subordinate keywords from the title and snippet, and then weight them based on [TF-IDF](https://en.wikipedia.org/wiki/Tf%E2%80%93idf){:target="_blank"}, dwell time and other factors. For results the user skipped, we would do sometime similar but apply negative weights. We used [stemming](https://en.wikipedia.org/wiki/Stemming){:target="_blank"}, [WordNet](https://en.wikipedia.org/wiki/WordNet){:target="_blank"} and clustering to then build semantic relationships between inferred intent and search results. There were even button to enable users to tweak the subordinate keywords by, among other things, adjusting their weights. The search results themselves were then reordered, in real time, based on the additional information about user intent gleaned from observing behavior and expressed via the 'invisible' weighted terms.

The end result was an adaptive search UI where results were re-ranked dynamically using a real-time personalization model built from inferred intent. The performance of the system was impressive, with users demonstrating [significant preference](link to more pudding) for dynamically ranked results over the baseline Google or eBay.

## Bye-bye guts

History is filled with products aiming to deliver a super user experience by offering buttons, knobs and sliders. With the exception of some specific parametric product search, they almost all fail. In particular, I'm reminded of [Yahoo! Mindset](https://www.seroundtable.com/archives/002003.html){:target="_blank"}, which was presented to me by a potential angel investor in Rank Dynamics. (He did not invest.) It was an experimental search interface that offered a [slider](https://www.cnet.com/culture/yahoos-slide-into-new-search/){:target="_blank"} to let "people reconfigure results on demand.. to display more commerical [sic] or more research-focused sites." Given my experience with Rank Dynamics I quickly identified that this would never work.

The [philosophy](link to 4 quadrants of personalization) that I developed was that implicit personalization is much more useful than explicit personalization because users either don't know their preferences or an not inclined to expend the effort to share and refine them. Furthermore, while long-term personalization can deliver value, real-time personalization is even more powerful because user preferences change very quickly and the half-life of most implicit preference signals can be measured in minutes.

The Rank Dynamics' sidebar disappeared very early on. While it was fun to 'see' what was happening down below, the information overwhelmed and confused users. What I learned from the experience is that that vast majority of users are not interested in knowing how the personalization is implemented and are certainly not inclined to make adjustments to the personalization factors. The MyMemoChat Memory sidebar will suffer the same fate.