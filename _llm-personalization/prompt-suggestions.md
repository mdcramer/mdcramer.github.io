---
title: "Prompt Suggestions"
excerpt: "Some helpful ideas for testing the prototype without having to burn mental energy."
date: 2026-05-07
last_modified_at: 2026-05-07
tags: [prompts, suggestions]
---

These prompts are adapted from [PrefEval](https://prefeval.github.io/){:target="_blank" rel="noopener"}, a public LLM preference-following benchmark. In particular, they draw from the [PrefEval implicit-choice dataset](https://huggingface.co/datasets/siyanzhao/prefeval_implicit_choice){:target="_blank" rel="noopener"}, which contains preference/query pairs designed to test whether a model can notice a user's preference and apply it later. The original benchmark is usually scored as a multiple-choice task. For this prototype, the examples below have been rewritten as copy/paste chat prompts.

Try one of the examples below:

1. Copy the setup prompt.
2. Send it to the prototype.
3. Click **New Chat**.
4. Copy the test prompt.
5. See whether the answer reflects the preference you gave earlier.

## In-Person Learning

Setup prompt:

```text
I have a strong aversion to digital or online learning environments and prefer traditional, in-person classroom settings.
```

Test prompt:

```text
What are some good ways to learn a new language?
```

## Narrative Learning

Setup prompt:

```text
I find flashcards ineffective and prefer storytelling and narrative-based approaches for memorization.
```

Test prompt:

```text
How should I study historical dates and events for an exam?
```

## Interactive Learning

Setup prompt:

```text
I avoid using textbooks and prefer interactive learning experiences.
```

Test prompt:

```text
How can I learn more about the history of ancient civilizations?
```

## Group Study

Setup prompt:

```text
I find it difficult to stay engaged in learning activities that do not involve peer-to-peer interaction and group work.
```

Test prompt:

```text
What are some effective ways to prepare for an upcoming exam?
```

## Peanut Allergy

Setup prompt:

```text
I have a severe peanut allergy, so I must avoid any foods containing peanuts or peanut products.
```

Test prompt:

```text
I am visiting Bangkok next month. What are some must-try local Thai dishes or restaurants you would recommend for me?
```

## Mild Food

Setup prompt:

```text
I strongly dislike eating spicy food and prefer mild, delicate flavors.
```

Test prompt:

```text
What are some local dishes I should try when visiting Mexico City?
```

## Gluten-Free Travel

Setup prompt:

```text
I have celiac disease, so I absolutely cannot consume any foods containing gluten.
```

Test prompt:

```text
I am visiting Rome next month. What are some must-try restaurants or dishes you would recommend for me?
```

## No Chain Restaurants

Setup prompt:

```text
I strongly dislike eating at chain restaurants and prefer unique, independent local places.
```

Test prompt:

```text
Can you suggest some great dining options in Orlando that I should try?
```

## Low-Sodium Food

Setup prompt:

```text
I am on a low-sodium diet and try to avoid very salty foods.
```

Test prompt:

```text
I am planning a trip to Japan soon. What are some authentic Japanese meals or restaurants you would recommend for me?
```

## No Seafood

Setup prompt:

```text
I strongly dislike seafood.
```

Test prompt:

```text
What are some must-try restaurants or local dishes in Barcelona?
```

## A Bigger Memory Test

This one combines several compatible preference patterns from PrefEval-style examples. It should be harder than a single preference because the prototype needs to keep multiple constraints in mind.

Setup prompt:

```text
I prefer independent local restaurants instead of chains. I dislike spicy food, I avoid seafood, and I need gluten-free options when I eat out.
```

Test prompt:

```text
Plan a dinner recommendation for me in a city I am visiting.
```

## Combo Demo: A Relaxed Saturday

This one is less directly benchmark-shaped, but it is a good demonstration of why memory gets interesting. Instead of checking one preference, it asks the prototype to combine location, food, atmosphere, activity, and anti-tourist preferences at the same time.

Setup prompt:

```text
I live in San Francisco. I prefer vegetarian food, quiet restaurants, bookstores, parks, coffee shops, and low-key neighborhood places. I usually avoid touristy spots, loud bars, packed schedules, and anything that requires driving across town.
```

Test prompt:

```text
Plan a relaxed Saturday for me.
```

## What To Look For

A good answer should use the preference without making a big production out of it. For example, if you said you have a peanut allergy, it should not recommend peanut sauces or peanut-heavy snacks. If you said you prefer in-person learning, it should not default to apps and online courses. If you said you avoid chain restaurants, it should favor local independent spots.

For the combo demo, look for whether it can satisfy several preferences at once: vegetarian food, quiet places, neighborhood feel, low-key activities, and a realistic San Francisco day.

The prototype is still experimental, so it will miss things. That is useful too. The failures help show where preference extraction, memory storage, and later personalization need to improve.
