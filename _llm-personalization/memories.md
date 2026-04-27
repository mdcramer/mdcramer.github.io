---
title: "Making memories"
excerpt: "Extracting user preferences from the prompts and then intelligently decaying them."
date: 2026-04-26 15:45:00
last_modified_at: 2026-04-26
tags: [memory, memories, decay]
---

After getting the [setup](/llm-personalization/setup/), the next set was representing what it learns about the user. For now, I have focused on a very specific kind of memory: **preferences**. The system is not yet trying to build a complete user model with biographical facts or long-lived profile information (more below). Instead, it is looking for preference signals in the user’s prompts and using those signals as the first layer of personalization.

This was a deliberate choice to mirror the [real-time implicit personalization](/rank-dynamics/selected-for-oral-presentation-at-sigir-09/){:target="_blank"} we worked on at [Rank Dynamics](/rank-dynamics/){:target="_blank"}. The goal is to observe signals that emerge during interaction and use them quickly to change future behavior.

## Extracting preferences

The first step is extracting preferences from the prompts. This is accomplished with a separate backend LLM call whose job is intentionally narrow: return a JSON object with two arrays, likes and dislikes, each containing short text snippets. If the user says something like "I like strawberries but I don’t like very sweet desserts," the extractor attempts to isolate those preferences and store them as separate memory items.

The current system is not trying to infer personality traits, stable facts or complex emotional states. It is only trying to catch reasonably clear preference evidence which makes the behavior easier to inspect and debug. Eventually, I will expand to include factual memories about the user as well. Facts, such as where a user lives, what they do for work, or what project they are working on, is not the same as a taste or preference and, as such, should probably decay much more slowly.

## What's the vector, Victor?

Once a preference is extracted, it is converted into a vector representation using OpenAI embeddings. An important design choice here is that the embedded text is normalized to the semantic content of the preference rather than the full surface form. In other words, the goal is to embed something like “strawberries,” not “I like strawberries” or “I dislike strawberries.” The signed weight is stored separately.

This matters because I want positive and negative evidence about the same concept to land in roughly the same part of vector space. If the user says “I like strawberries” in one moment and “I don’t like strawberries” in another, the prototype should treat those as two pieces of evidence about the same underlying topic, not as unrelated memories. The vector is meant to capture semantic similarity, while the weight captures direction and strength.

At the moment, those weights are simple. Preferences are stored with signed values and the decay behavior is configurable, but I have not yet built the more intelligent weighting scheme that I ultimately want. For now, the important thing is that the prototype already separates semantic representation from preference direction, which gives it a useful structure for future refinement.

## Clustering related memories

Once memories are embedded, the next task is grouping related ones together. For this, I chose DBSCAN because it does not require pre-specifying the number of clusters, like [k-means](/apple-2-blog/k-means/){:target="_blank"}. That is attractive because the number of memory themes depends on the user’s behavior rather than on an arbitrary design decision. If the user has expressed many related preferences, clusters should emerge naturally. If not, memories remain unclustered.

Conceptually, the clustering step is meant to discover topics of preference rather than isolated statements. A user may express the same taste repeatedly in slightly different ways, or may express related attitudes toward a broader concept. Clustering makes it possible to start treating those as part of a shared pattern rather than as independent rows in a database.

This is also where the prototype begins to move beyond simple prompt injection. Instead of just remembering isolated likes and dislikes, it starts building grouped preference areas. That is important because a personalized system should ideally react not just to exact repetition, but to related evidence that accumulates over time.

## A cluster by any other name...

A cluster of vectors is useful computationally, but for the system to use clustered memories in prompt injection, and for the interface to make sense to users, each cluster needs a readable description.

The current approach sends the aggregated cluster memories, along with their signed scores, to the LLM and asks it to generate a short directional description. In contrast to the memoires, the prompt explicitly asks the model to infer the underlying preference direction that best explains the cluster as a whole. So the goal is not merely to name a concept like “mechanical keyboards,” but to produce something more like a preference description, such as a preference for quieter keyboard sounds or a dislike of loud, clicky ones.

The prompt also asks the model to judge whether each memory in the cluster supports or opposes the final cluster description. That matters because positive and negative memories about related concepts may still point toward the same higher-level preference. This gives the prototype a first pass at interpreting preference structure rather than merely storing raw observations.

## Real-time signals, not full identity

One thing worth emphasizing is that this is still a very lightweight memory system. It is not trying to become a deep, persistent identity model of the user. That may come later in some form, especially once factual memories are added, but the current behavior is closer to short-horizon adaptation. In that sense, it remains aligned with the older Rank Dynamics intuition of using immediate interaction signals to improve relevance in real time.

That is also why decay matters. Some memories should fade if they are not reinforced. Others should become stronger as evidence accumulates. At the moment the decay mechanism is still relatively blunt, and one of the next steps will be to make those decay weights more intelligent. I expect factual memories, when introduced, to behave very differently from preference memories in this respect.

## Prompt injection today and tomorrow

Right now, the prompt injection layer is still simple. The system stores and clusters the memories, but the live chat prompt is still primarily injected with raw remembered likes and dislikes when they seem relevant. In other words, the more sophisticated cluster descriptions already exist, but they are not yet the main representation used to guide the assistant.

That will eventually change. The direction I want to move in is to inject cluster-level natural language descriptions, augmented with some sense of weight or confidence. Instead of giving the model a flat list of remembered items, the prompt could communicate higher-level preference summaries such as strong tendencies, mild tendencies or mixed evidence around a topic. That would be much closer to the kind of structured, interpretable personalization I have in mind.

For now, the prototype is in an intermediate and useful state. It can extract preferences, map them into vector space, cluster related memories and generate directional descriptions for those clusters. That is already enough to make the memory system feel less like a bag of saved strings and more like the beginnings of a personalized representation of user intent.