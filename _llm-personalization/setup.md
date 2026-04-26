---
title: "Setup"
excerpt: "Some background into how I got the prototype off the ground."
date: 2026-04-26
last_modified_at: 2026-04-26
tags: [setup, streaming, API, DNS]
---

After laying out the [motivation](/llm-personalization/motivation/), the next question was how to build something simple enough to experiment with but real enough to share.

I did not want a heavy framework or a complex cloud architecture. The goal was not to build a polished product but a working prototype that would let me explore personalization in a concrete way. That meant choosing tools that were familiar, lightweight and easy to modify.

The basic stack ended up being:
- a single-page frontend in HTML and JavaScript,
- a small Python backend using Flask,
- OpenAI's API for the model calls and
- SQLite for local storage.
The idea was to keep the application legible. I wanted to be able to understand the whole system, change individual pieces quickly, and avoid spending the early days of the project fighting the scaffolding.

## To stream or not to stream

I also chose not to implement streaming at the outset. That was partly a product decision and partly an architectural one. Since I wanted to work in a stack I already knew well, I started with a very simple HTML/JavaScript frontend and a Python Flask backend. Streaming would have been possible in that setup but it would have added complexity and pulled attention toward interface polish rather than the core question of the project. The memory logic is the story, so I kept the interaction loop simple and focused development effort there.

## My coding partner, Codex

Codex was my development partner. Rather than writing everything [from scratch](https://mortalwayfare.com/building-the-game-engine-from-scratch/){:target="_blank"} in the traditional way, I used Codex conversationally to sketch the initial structure, generate and revise code, troubleshoot issues, and iteratively add features. That ended up shaping not just the speed of development, but the style of it. Instead of trying to design the entire system up front, I moved in small steps, testing each change and then deciding what to do next. My experience with coding agents is that, like when developing something from scratch, it helps to break the project up into little pieces and stage them out. For a prototype like this, that worked extremely well.

## Bare bones

The first version was intentionally minimal. Before worrying about memory, embeddings, clustering or prompt injection, I just wanted a chatbot that worked. The frontend sends a message to the Flask backend, the backend forwards the request to OpenAI, and the response comes back to the browser. That simple loop established the core application shape and made it possible to layer in personalization later without rethinking everything.

To make that work, I needed an OpenAI API key. A ChatGPT subscription is not the same thing as API access, so I created an API key through the OpenAI platform, configured billing and stored the key as an environment variable rather than hardcoding it into the project in order to cleanly separate the application code from credentials and make it easier to run the same project locally and in production.

Local development was done the old-fashioned way, on localhost. I used a familiar Conda-based Python environment, installed the dependencies, ran the Flask app and iterated from there. This made it easy to test changes quickly and keep the feedback loop short.

## Sharing with the world

Once the `127.0.0.1:5000` local version was stable enough to be interesting, I wanted to put it online so that other people could try it. For hosting, I chose Railway for its simplicity. Railway connects straight to a GitHub repository so changes are deployed automatically with a simple `git push`. There was no need to build a deployment pipeline from scratch or think deeply about servers. I just needed a reliable way to turn a local experiment into a public URL.

The application also needed a little production-minded handling because it uses SQLite. On a local machine, SQLite is almost effortless. In the cloud, it raises the practical questions of where does the database live, and does it survive restarts and redeploys? Railway's persistent volume support provided a clean answer that let me keep the lightweight local-database approach while still preserving the prototype’s memory store across deployments.

Once the app was live on Railway, the next step was to make it feel less temporary with a custom domain name. (I bought [mymemochat.com](https://mymemochat.com){:target="_blank"} because it was available and I didn't feel like spending days thinking about this.) This, unfortunately, turned out to be one of the more finicky parts of the setup. The DNS provided by the company hosting my domain did not play nicely with Railway's custom-domain and SSL flow, particularly at the root. Railway expects a CNAME-style setup and some providers’ ALIAS-style behavior is unreliable for this because Railway services sit behind dynamic shared IPs. The practical fix was to move DNS handling to Cloudflare. That solved two problems at once:
1. Cloudflare supports CNAME flattening at the root domain and
2. it gave me a more predictable path for SSL.

## Getting to work

One thing I appreciated about this setup is that it preserved the same basic development rhythm. I could still work locally on 127.0.0.1, test changes quickly, and only push when something was ready to be seen publicly. Once the code was pushed to GitHub, Railway would redeploy the updated app. That created a smooth bridge between experimentation and publication, which is what I wanted.

This all may sound ordinary, but when building a prototype whose main novelty lies in behavior rather than infrastructure, there is real value in keeping the surrounding system boring. A simple frontend, a small Flask backend, an API key, a local database, a straightforward host and a custom domain were enough to get the project to the point where the more interesting questions could begin.

Those more interesting questions are really what the project is about. Once the basic shell was in place, I could start focusing on the personalization itself: how memories should be extracted, represented, weighted, clustered, decayed and eventually injected back into future prompts.