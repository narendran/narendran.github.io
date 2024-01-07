---
layout: post
comments: true
title:  "Learning Logs: 2024-01-06"
category: "learning"
excerpt: "Mix of LLM industry, politics, general deep learning and quotes on importance of prioritization and focus"
date:   2024-01-06 10:00:00
---

Summary: 

## Industry News

* OpenAI is launching the first-in-industry **GPT store** next week. [Ref](https://twitter.com/rowancheung/status/1742967393310368222?s=20&utm_source=www.therundown.ai&utm_medium=newsletter&utm_campaign=openai-s-gpt-store-plans-revealed). Google *might* be having similar plans with [advanced Bard](https://www.theverge.com/2024/1/4/24025270/google-bard-advanced-paid-subscription) based on Gemini Ultra. Other interesting things from OpenAI: 30B -> 90B market cap in 2023, deal for real-time news with Axel Springer who among other things owns Business Insider, Politico etc. Personal thought: These kinds of **revenue sharing agreements** from BigTech, will create disproportionate benefit for those with big distributions already (e.g. Apple) and will effectively seal the position of BigTEch in the "LLMs for information/news" space.

## Politics / US

* Expecting a Republican win in 2024, not that I am rooting for it, just what I am seeing from polls. Democrats had a wonderful opportunity to bring in a strong candidate but failed, and in fact their alleged campaign to keep Trump in the radar has backfired.
* International:
  * Argentina is not joining **BRICS**. Sacks: Milei is pro-West and pro-Israel, its not surprising they are not joining BRICS. Side note: BRICS was originally formed by Brazil, Russia, India and China in 2009, South Africa joined a year later in 2010. Big expansion in Jan 1, 2024 when Egypt, Ethipia, Iran, Saudi Arabia and UAE have joined.
  * **Wars**: Russia is making strong progress, Volodymyr Zelenskyy is not able to get much traction in US. US wants to stop the war, but Zelenskyy has lost ground and won't stop until getting back. The way things are, Russia might make more gains into Ukraine. Once again, no interests here, just observing.
  * **Petrodollar** at risk: In March 2023, Saudi Arabia started accepting Yuan for Chinese oil purchases, and then US countered with a deal for military protection and nuclear development in exchange for distancing Saudi from China. Note, the connection with strengthening BRICS above.
* In 2024, the federal funding to boost **broadband connectivity in underserved communities** will start rolling out. Program name is Broadband Equity, Access and Deployment (BEAD), and deploys $42.45B ([Tech brew article](https://www.emergingtechbrew.com/stories/2024/01/04/2024-us-broadband-funding?mbcid=33893026.233544&mblid=f8dd3cb5addb&mid=344734a49289e50cb952e4cce2ea389e&utm_campaign=etb&utm_medium=newsletter&utm_source=morning_brew))

## GenAI capabilities

* Personal experience: **DALL-E** couldn't make targered, local corrections to the logo generated -- this is while I was building a CustomGPT. While it does follow the instructions, it changes other aspects of the image like unrelated background, sizes and shapes of objects.
* Custom GPTs are working *very* well. E.g. I did a test with the book "Success vs. Joy", and it excerpted the exact three lines which talk about that question on meaning of life. This is like talking to **someone who has read the whole book**!

## Deep learning

* Had a good revision of how we arrived at **modern neural recommender models** from [ML Frontiers substack](https://mlfrontiers.substack.com/p/machine-learning-frontiers-in-2023). Following are some paradigm shifts we've had: At least until 2016, matrix factorization was the top collaborative filtering technique, then in 2016-17, we had the Neural Collaborative Filtering and Wide And Deep Networks from Google, the latter pretty much set the stage for all improvements until the 2023 SOTA architectures. The deep part was essentially taking the sparse representations of user features (profile text, user embeddings, recent history, user interests etc.) and item features (description text, title text etc.) and getting embeddings for each of the individual features, and passing them through a multi-layer feed-forward network to return a vector or number finally. This part has not changed much. The "wide" part which is where the raw features are exposed directly to the final layer, and this is where most improvements have happened -- for instance, Wide and Deep models paper suggested doing the crosses and then feeding to the model, and then DCN introduced finding crosses automatically, DeepFM converted the feature crosses into dot products, AutoInt said using multi-head attention can learn interactions better etc.

## Quotes

On the importance of systems, prioritization and focus:
* "Most of what we say and do is not essential. If you can eliminate it, you’ll have more time, and more tranquility. Ask yourself at every moment, **‘Is this necessary?’**" -- *Meditations* by Marcus Aurelius.
* "We are told that life is short and the art is long... It is not that we have a short time to live, but that we waste a lot of it. Life is long enough and a sufficiently generous amount of it has been given to us for the highest achievement if it were all well invested. When it is wasted in the heedless luxury and spent on no good activity, we are forced at last by death’s final constraint to realize that it has passed away before we knew it was passing. **So it is: we are not given a short life, but we make it short.** We are not ill supplied but wasteful of it. Just as when ample and princely wealth falls to a bad owner it is squandered in a moment, but wealth however modest, if entrusted to a good custodian, increases with use, so our lifetime extends amply if you manage it properly." -- *On the Shortness of Life: Life Is Long if You Know How to Use* It by Seneca
* "Goals are good for setting a direction but **systems are best for making progress**." -- James Clear
* "As soon as we control where awareness goes we control where energy flows. As soon as we control where energy is flowing we control what is manifesting in our life. And we need willpower and our powers of concentration to direct awareness." -- Unwavering Focus by Dandapani