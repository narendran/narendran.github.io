---
layout: post
comments: true
title:  "Learning Logs: 2024-01-04"
category: "learning"
excerpt: "LLMs and medicines"
date:   2024-01-04 10:00:00
---

## LLMs

* [Depthwise UpScaling (DUS)](https://arxiv.org/pdf/2312.15166.pdf) starts with a n-layer model and keeps iteratively duplicating + concatenating the encoder stacks from that same LLM. Alternative to MoE for **scaling up base models**.
* As of end of 2023, "memorization", where the LLMs output entire sequences from their training data verbatim, is still not solved.
* In 2023, LLM startups: **EleutherAI** continue to publish prolifically in the interpretability and LLM controllability spaces. E.g. Pythia platform + suite of models and training details like model architecture and learning rates.
* In 2023, **Open Source LLMs**: Llama2 was a game changer, despite the 70B variant being bested by Mixtral 8x7B, Yi34B and DeepSeek-67B on public benchmarks. Mistral 7B base model, Zephyr 7B with DPO finetuning, Mixtral-7B and Mixtral-7B-Instruct are leading the OS models. Phi, 1.5 and 2 are powerful "very" small LLMs in 1B-3B parameter regime with textbook quality datasets which beat the Llama2 7B, continuing to show the importance of high quality datasets.
* In 2023, LLMs and trustworthiness of benchmarks -- because LLMs have seen those datasets already.
* Finetuning improvements: [**QLORA**](https://arxiv.org/pdf/2305.14314.pdf), which is quite literally "quantized" version of LORA, can reduce GPU memory overhead by 1/3 while increasing runtime the same amount. Finetuning a 7B parameter model on AWS costs about 100$ and is done in 5-7 hours for few 1000 examples.

## Medicines

* **ADHD**: Adderall used to treat ADHD, 41.4M prescriptions in 2021 -- projecting to be ~60M now. So close to 1 in 5 people in US.
* **Sleep**: Back in 2020, 8.4% of adults had used sleep medications according to National Center of Health Statistics report. So possibly 1 in 10 people use it now?
* **Weight loss**: We learnt that doctors have been prescribing Ozempic for weight loss since 2017 -- and it works by making you eat less sugar by mimicking a gut hormone called GLP-1 which tells your brain that you don't need more sugar, and also keeps the food in our stomach longer. The argument for obesity to be a disease is calling obesity "a matter of mismatched signals between the brain and body" and that Ozempic and similar GLP-1 mimicking drugs are the medicines for that disease. Other counterparts: Wegovy and Mounjaro. Previous attempts include Belviq, which was pulled back in 2020 due to increased cancer risk. Estimate of penetration: ~3M, or close to 1 in 100 people in USA.