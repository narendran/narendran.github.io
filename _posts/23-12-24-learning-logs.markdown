---
layout: post
comments: true
title:  "Learning Logs: 2023-12-24"
category: "learning"
excerpt: "Testing out a new format to share what I read on a weekly basis"
date:   2023-12-24 00:00:00
---

Starting an experimental series where I share my weekly learnings across various domains of interest.

## Machine Learning

### GenAI
* What's up with Mixtral? Its the first 8 X 7B parameter count, sparse MoE open source model ([HF model card](https://huggingface.co/mistralai/Mixtral-8x7B-v0.1)), and the second model from Mistral AI after Mistral. Mistral AI is the Paris based "LLM models and platform" startup, currently at 2 rounds of funding and valuation at $2B valuation, with a 22-person team. We can play with it in HF after transformers version 4.36.
* LLM Self-reflection in Dec 2023: Impressive work by Guardrails AI team on building the right primitives of "rails" for spec and "guard" for enforcing, and building abstractions like validators on top of it. Highly useful to a wide range of LLM applications. [Link](https://www.guardrailsai.com/)
* Apple LLMs:
  * [Ferret](https://arxiv.org/pdf/2310.07704.pdf) from Apple, 7B/13B multi-modal LLM which enables any-form referring and grounding into a single model. Tricks: hybrid region representation (discrete coordinates + continuous features via spatial-aware visual sampler).
  * [LLMs in a Flash](https://arxiv.org/pdf/2312.11514.pdf) introduces ideas to serve LLM with a combination of Flash and DRAM memory. Firstly, it reduces the amount of data to transfer from Flash to DRAM, and secondly to move them efficiently using "windowing" and "row-column bundling".
* [Thought] 2024 will be the year of smaller, more domain-focused LLMs?

## Other ML
* Tomas Mikolov won the Test of Time Award for his 2013 paper (with other Google colleagues) on word2vec ([paper](https://papers.nips.cc/paper_files/paper/2013/hash/9aa42b31882ec039965f3c4923ce901b-Abstract.html)).

## Industry / Business

* Databricks LLM MOAT: Best in class LLM inference for SOTA open source models like Llama2 and Mixtral? Ref: [Databricks + NVIDIA TensorRT-LLM](https://www.databricks.com/blog/Integrating-NVIDIA-TensorRT-LLM)
