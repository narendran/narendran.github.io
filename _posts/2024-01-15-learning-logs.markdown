---
layout: post
comments: true
title:  "Learning Logs, Information Sources: 2024-01-19"
category: "learning"
excerpt: "Testing out a new format to share what I read on a weekly basis"
date:   2024-01-19 10:00:00
---

## LLMs

**Startups on LLM hosting**
* Fireworks.ai: Competetive advantage with inference speed, simple APIs, lower cost, leading to faster iteration speed. Data security: SOC2 and HIPAA compliance. Floating point quantization is better than integer quantization. Current consensus is that FP8 is the best on latency vs. quality tradeoffs. [[fireworks.ai blog](https://app.fireworks.ai/blog/fire-attention-serving-open-source-models-4x-faster-than-vllm-by-quantizing-with-no-tradeoffs)]
* Inference speeds
    * Llama2-7B-Chat (TTFT is ~800ms @ 8 TPS)
    * Llama70B-Chat (TTFT is 276ms, TPS: 50 TPS)
    * Mistral-7B-Instruct (TTFT is ~300ms @ 91 TPS)
    * Mixtral-7B-Instruct (TTFT is ~341ms @ 105 TPS)


**Trust and Safety**:
* [TrustLLMs](https://arxiv.org/pdf/2401.05561.pdf) from 70+ authors from dozens of organizations define trustworthiness on 8 dimensions and 6 benchmarks. Show the importance of AI alliance including industry, adacemia and open-source models.
* Similarly, Anthropic AI released [Sleeper Agents](https://arxiv.org/pdf/2401.05566.pdf) which shows if a bad actor has released a base model with a backdoor, no amount of finetuning or RLHF safety mechanisms can completetely remove the backdoor.

**Speed of adoption**:
* Military & Defense: OpenAI removes clause to not use ChatGPT from military use.
* Consumer devices: Humane AI pin, [Rabbit R1](https://www.wired.com/story/rabbit-r1/?utm_source=www.turingpost.com&utm_medium=newsletter&utm_campaign=fod-37-trust-but-verify) which is a 2.88-inch touchscreen device which uses ChatGPT to understand our request and their own Language Action Models which do the actual work. The skills are learnt by the model "looking" at how actions are done in web/mobile and replaying them for other tasks.
