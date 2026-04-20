---
title: "Motivation"
excerpt: "Motivation for building a prototype for chatbot personalization."
date: 2026-04-19
last_modified_at: 2026-04-19
tags: [motivation]
---

At [Rank Dynamics](/rank-dynamics){:target="_blank"}, our team worked on the problem of real-time personalization in search. The idea was simple: a short query rarely captures a person’s true intent and static ranking does a poor job of adapting as that intent becomes clearer. We believed relevance should not be frozen at the moment the query is issued but rather improved as the system learns, implicitly, from the user's actions.

The core problem was [too many search results](/rank-dynamics/the-problem-too-many-results/){:target="_blank"}. In their paper entitled “Beyond the Commons: Investigating the Value of Personalizing Web Search,” Teevan et al. make the observation that:

> “Web queries are very short, and it is unlikely that a two- or three-word query can unambiguously describe a user’s informational goal.”

As such, we laid out our philosophy for addressing this problem with [four quadrants of personalization](/rank-dynamics/the-four-quadrants-of-personalization/){:target="_blank"}. First, information regarding user intent can be learned explicity (thourgh keyword entry) and implicitly (through actions and inactions). In particular contexts, like deep research and [shopping](/rank-dynamics/more-pudding/){:target="_blank"}, the implicity signals turned out to be the most powerful. Addtionally, however, signals about a user's intent have a half-life. Some aspects of personalization don't change frequently but most signals should decay quickly. As a segue from search to LLMs, Andrj Karpathy recently [wrote](https://x.com/karpathy/status/2036836816654147718){:target="_blank"}:

> "One common issue with personalization in all LLMs is how distracting memory seems to be for the models. A single question from 2 months ago about some topic can keep coming up as some kind of a deep interest of mine with undue mentions in perpetuity. Some kind of trying too hard."

Large language models (LLMs) make this old philosophy newly interesting.

LLMs are often discussed as if they have replaced search, which feels true to a large extent. In practice, however, they inherit many of the same problems, which are, frankly, fundamental to communication. The interface is more fluid and the output is more polished but the system still has to infer what the user actually wants. In fact, the problem may be even harder now. Instead of choosing which ten links to rank at the top, the system is choosing how to frame an answer, what assumptions to make, which facts to emphasize, how much detail to provide and what tone or style best fits the moment.

A beginner and an expert may need very different explanations of the same idea. A user who prefers concise answers may experience the same response differently from someone who wants more context. A recommendation that is technically sound may still feel wrong if it conflicts with a person’s tastes, habits or current goals. To Andrej's point, bringing up old signals after the person has moved on can be frustration. What matters is not only whether the model can generate a plausible response, but whether it can generate one that feels appropriately aligned to a particular user at a particular moment.

So, over a weekend I built www.mymemochat.com.

It's a prototype that looks reminiscent of an early Rank Dynamics prototype. (I wish I had saved a screenshot!) We eventually dropped the 'insights' in the left panel and then quickly moved to delivering our technology through a browser extension (which ended up being installed tens of millions of times) but it makes the process transparent which helps with debugging and communicating the value proposition.

The whole thing was built with Codex using OpanAI GPT-4o mini on the backend. The current implemention progressively layers personalization on top on the LLM through prompt injection, using a local embedding vector memory store and explicit logic for deciding what should be saved, reinforced, decayed or discarded. Unlike some [other projects](https://www.mortalwayfare.com){:target="_blank"}, I didn't write a line of code. That being said, I had a plan from the beginning and broken the development into small chunks. I'll describe those in future posts.

In the meantime, give it a go and let me know what you think.