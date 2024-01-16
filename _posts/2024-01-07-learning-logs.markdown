---
layout: post
comments: true
title:  "Learning Logs: 2024-01-07"
category: "learning"
excerpt: "Some LC coding, and reading on pace layering and the ability of complex systems to exhibit contradictory properties"
date:   2024-01-07 10:00:00
---

## Programming
* On Jan 7th, I felt like revising my coding skills on leetcode. As much as I hate them, I couldn't find a better way to "exercise" the part of my brain which does small-scale, closed-form problem solving, mental-model/ds/algorithms mapping, remembering constraints and writing good, testable and extensible code. I stated with an easy, then did a couple of mediums -- all randomly selected by LC.
* I needed to use Spark at work to scale an operation from a notebook to a much larger scale for production usecases. I learnt about Spark's Client mode vs. Cluster mode, the speed of development with Client mode and the pain of python version mismatches in client mode. Learnt that sentence-transformers do not work with Python 2.7, which means I had to redo a bunch of spark executions which takes a longer time to complete on cluster mode.

## Industry
* Apple has pulled nine crypto exchanges including Binance from its App Store in India after a couple of weeks of the Financial Intelligence Unit of India serving notices to those companies for illegal operation in the country violating anti-money-laundering rules. [TC](https://techcrunch.com/2024/01/09/apple-crypto-apps-binance-india/).

## Work-Life
* "If you only read the books that everyone else is reading, you can only think what everyone else is thinking." - Haruki Murakami's Norwegian Wood.
* [Pace Layering](https://jods.mitpress.mit.edu/pub/issue3-brand/release/2?utm_source=substack&utm_medium=email): How complex systems are built to be strong and flexible at the same time? The contradicting properties are coming from different layers of the system. The velocity comes from the outermost, high-speed, highly-flexible layer and the stability comes from the lower layers. For a single human being, I would say this ultimately comes from values and experiences -- which form convictions -- which leads to decisions in 2-3 layers. **What is important to understand is that, what we do at the outermost layer has meaningful impact on the inner layers over time.** Hence the importance of actively focusing on what we do everyday -- its noise if it happens one day, its a pattern and makes L-1 layer changes with sustained practice. With time, it could compromise the fundamental value system layers.
* On pace layering, a very good quote about how human beings coming into existence is on layers of time scale: *"The destiny of our species is shaped by the imperatives of survival on six distinct time scales. To survive means to compete successfully on all six time scales. But the unit of survival is different at each of the six time scales.
  * On a time scale of years, the unit is the individual.
  * On a time scale of decades, the unit is the family.
  * On a time scale of centuries, the unit is the tribe or nation.
  * On a time scale of millennia, the unit is the culture.
  * On a time scale of tens of millennia, the unit is the species.
  * On a time scale of eons, the unit is the whole web of life on our planet.
  Every human being is the product of adaptation to the demands of all six time scales. That is why conflicting loyalties are deep in our nature. In order to survive, we have needed to be loyal to ourselves, to our families, to our tribes, to our cultures, to our species, to our planet. If our psychological impulses are complicated, it is because they were shaped by complicated and conflicting demands"* -- Freeman Dyson
