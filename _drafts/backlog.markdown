Longer contexts in LLMs
* Actually start with why? https://ai.stanford.edu/blog/longer-sequences-next-leap-ai/
* Problem space: World's LLMs are still using Transformers whose computational complexity increases quadratically with sequence length. Why? Because the interaction layer in Transformers is a Multi-Headed Attention layer where each Attention block is a scaled, softmax self-attention layer.
* Ref: https://medium.com/@geronimo7/mamba-a-shallow-dive-into-a-new-architecture-for-llms-54c70ade5957
* Could State Space Models be the new architecture for LLMs? Mamba is the experiment showing 4X inference throughput at reduced world knowledge and instruction following is on par with TinyLlama which is transformer based.
* Alignment with in-context learning only:
* Model training: Backpropagation in neural networks.


In 2023:
* Alternatives to Transformers: [Receptance Weighted Key Value (RWKV)](https://arxiv.org/abs/2305.13048) from EleutherAI which uses a linear-scaling token interaction using "channel-directed attention".