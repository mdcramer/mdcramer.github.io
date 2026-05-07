---
title: "Philosophical first principles"
excerpt: "How I think about personalization in general and personalizing LLMs in particular."
date: 2026-05-06 14:00:00
last_modified_at: 2026-05-06
tags: [personalization, philosophy, implicit, explicit, decay]
---

When building [mymemochat.com](http://mymemochat.com/){:target="_blank"}, I started from philosophical first principles of personalization. I discussed some briefly under [Motivation](/llm-personalization/motivation/) but I'll make them explicit here.

## Problem

As difficult as it is for users to unambiguously express their intent to a search engine through a set of keywords, it is virtually impossible to do so through a prompt to an LLM, regardless of the size of the context window. At [Rank Dynamics](/rank-dynamics) we addressed the former with real-time [personalization](/rank-dynamics/the-four-quadrants-of-personalization) through a model of inferred intent gleaned from implicit signals. With this prototype I hope to demonstrate some of the same thinking applied to an LLM.

## Key principles

There are a few things which I believe are universally true:

1. **Implicit signals are more powerful than explicit signals** - Both are very [useful](/rank-dynamics/dont-ask-just-do-it), but not only are implicit signals more abundant, users are frequently unable to explicitly express their preferences because they don't know they have them. When Dr. Usama Fayyad, Yahoo!'s EVP of Research & Strategic Data Solutions, [said](https://www.tmcnet.com/usubmit/2007/04/16/2510402.htm){:target="_blank"}, "I know more about your intent than any 1,000 keywords you could type," he was making the point that behavioral signals reveal intent that explicit inputs never capture. This continues to be true today.

2. **Preferences decay** - While some [decay](/rank-dynamics/hold-the-pickles-hold-the-lettuce) faster than others, all inferred preferences lose predictive power over time. A key distinction is between *modes* and *facts*. Modes (car shopping, travel planning, job searching) are behavioral states that have a short half-life by nature and should decay quickly regardless of what happens next. Facts ("I live in SF," "I own a Honda Civic") decay slowly. Preferences fall somewhere in between. Crucially, systems should discover life changes through natural conversation as opposed to prompting users or mining external data sources.

3. **Preferences are not a point but a space** - Preferences have a natural hierarchy and are typically amorphous and overlapping. A signal about baseball relates to sports broadly. A signal about hiking relates to both fitness and the outdoors. This means a new memory can refresh the decay clock for not just an exact match but a neighborhood of semantically related memories, with influence attenuating by distance. The memory store behaves less like a flat list of facts and more like a weighted graph of embeddings. At Rank Dynamics we tokenized and stemmed content before applying [WordNet](/rank-dynamics/fast-easy-wordnet-java) to expand the semantic matching.

4. **Preference dissonance is natural** - Because preferences are amorphous and overlapping, apparent conflicts are common and usually not real conflicts. Users who live in both San Francisco and New York are not contradicting themselves. A user who loved baseball last year and says, "I no longer watch baseball" is providing a new signal that will outweigh the former one as the old one decays. No explicit conflict resolution is required. The LLM is smart enough to handle ambiguity at inference time. The system's job is to maintain a well-decayed memory store as opposed to adjudicate between competing beliefs. At Rank Dynamics we collected both [positive and negative](/rank-dynamics/evaluating-surf-canyons-technology-part-2/) preference signals which we simultaneously used to, respectively up-rank and down-rank results.

## Technical framework

Based on the principles above, the personalization system is designed around five steps:

1. **Extract** - After each interaction, the system identifies memorable signals: stated preferences, implicit behavioral cues, facts about the user and the mode they appear to be in. This happens automatically, without requiring the user to explicitly say "remember this."

2. **Embed** - Each memory is encoded as a dense vector embedding and stored in a local vector memory store. Representing memories as embeddings rather than discrete facts enables semantic retrieval and proximity-based refresh.

3. **Decay** - Every memory has a strength value that decays over time at a rate determined by its type. Modes decay fastest. Preferences decay at a moderate rate. Facts decay slowly. When a new signal arrives that is semantically related to an existing memory, the decay clock on that memory (and those nearby in the embedding space) is reset, with the refresh effect attenuating by semantic distance.

4. **Retrieve** - At inference time, the current prompt is encoded and used to query the memory store for the most semantically relevant, non-decayed memories. This is a standard RAG (retrieval-augmented generation) pattern. The retrieved memories are then injected into the prompt context before generation.

5. **Augment** - The LLM generates a response with the retrieved memories included in its context. No special fine-tuning or model modification is required. The personalization lives entirely in the memory pipeline rather than the model weights.

The result is a system that gets more useful the more you use it, forgets what's no longer relevant and never requires you to manage it explicitly. Future posts will walk through the implementation of each step in detail.