---
title: "Motivation"
excerpt: "Motivation for building a prototype for chatbot personalization."
date: 2026-04-19
last_modified_at: 2026-04-22
tags: [motivation]
---

At [Rank Dynamics](/rank-dynamics){:target="_blank"}, our team worked on the problem of real-time personalization in search. The idea was simple: a short query rarely captures a person’s true intent and static ranking does a poor job of adapting as that intent becomes clearer. We believed relevance should not be frozen at the moment the query is issued but rather improved as the system learns, implicitly, from the user's actions.

The core problem was [too many search results](/rank-dynamics/the-problem-too-many-results/){:target="_blank"}. [Teevan](https://www.microsoft.com/en-us/research/people/teevan/publications/){:target="_blank"} et al., in "Beyond the Commons: Investigating the Value of Personalizing Web Search," put it plainly:

> “Web queries are very short, and it is unlikely that a two- or three-word query can unambiguously describe a user’s informational goal.”

As such, we laid out our philosophy for addressing this problem with [four quadrants of personalization](/rank-dynamics/the-four-quadrants-of-personalization/){:target="_blank"}. The quadrants distinguish two axes: signals learned explicitly (through keyword entry) vs. implicitly (through actions and inactions) and those that are captured in real time vs. built up over the long term. In particular contexts, like deep research and [shopping](/rank-dynamics/more-pudding/){:target="_blank"}, the implicit signals turned out to be the most powerful. Critically, however, user intent signals have a half-life. Some aspects of personalization don't change frequently but most signals should decay quickly.

As a segue from search to LLMs, Andrej Karpathy recently [wrote](https://x.com/karpathy/status/2036836816654147718){:target="_blank"}:

> "One common issue with personalization in all LLMs is how distracting memory seems to be for the models. A single question from 2 months ago about some topic can keep coming up as some kind of a deep interest of mine with undue mentions in perpetuity. Some kind of trying too hard."

Large language models (LLMs) make this old philosophy newly interesting.

LLMs are often discussed as if they have replaced search, which feels true to a large extent. In practice, however, they inherit many of the same problems, which are, frankly, fundamental to communication. The interface is more fluid and the output is more polished but the system still has to infer what the user actually wants. In fact, the problem may be even harder now. Instead of choosing which ten links to rank at the top, the system is choosing how to frame an answer, what assumptions to make, which facts to emphasize, how much detail to provide and what tone or style best fits the moment.

A beginner and an expert may need very different explanations of the same idea. A user who prefers concise answers may experience the same response differently from someone who wants more context. A recommendation that is technically sound may still feel wrong if it conflicts with a person’s tastes, habits or current goals. To Andrej's point, bringing up old signals after the person has moved on can be frustrating. What matters is not only whether the model can generate a plausible response, but whether it can generate one that feels appropriately aligned to a particular user at a particular moment.

I wanted to test whether a lightweight system, built in a weekend, with no custom model training, could meaningfully personalize LLM responses by maintaining a small, decaying memory of what the user cares about and then selectively injecting that context at inference time.

So, over a weekend I built [mymemochat.com](https://mymemochat.com){:target="_blank"}.

It's a prototype that looks reminiscent of an early Rank Dynamics prototype. (I wish I had saved a screenshot!) We eventually dropped the 'insights' in the left panel and then quickly moved to delivering our technology through a browser extension (which ended up being installed tens of millions of times) but it makes the process transparent which helps with debugging and communicating the value proposition.

The whole thing was built with Codex using OpenAI GPT-4o mini on the backend. The system progressively layers personalization on top of the LLM through prompt injection, using a local embedding vector memory store and explicit logic for deciding what should be saved, reinforced, decayed or discarded. I used Codex as a development partner throughout, sketching the architecture myself and breaking it into small chunks, without writing a line of code directly.

In future posts, I'll walk through the architecture in detail: how memories are extracted and embedded, the decay logic, how RAG augmentation works in practice and what I'd do differently. In the meantime, give it a try and let me know what you think.