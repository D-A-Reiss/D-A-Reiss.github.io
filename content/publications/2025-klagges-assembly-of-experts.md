---
title: "Assembly of Experts: Linear-time construction of the Chimera LLM variants with emergent and adaptable behaviors"
date: 2025-05-31
draft: false
authors:
  - name: "Henrik Klagges et al. (incl. David A. Reiss)"
venue: "arXiv preprint arXiv:2506.14794"
year: 2025
arxiv: "https://arxiv.org/abs/2506.14794"
page: "https://huggingface.co/tngtech/DeepSeek-R1T-Chimera"
code: ""
selected: true
topics: ["AI"]
tags: ["large-language-models", "mixture-of-experts", "model-merging", "chimera"]
summary: Requiring 10^13-10^15 FLOPs to calculate one 8 bit weight in an LLM during pretraining is extremely expensive and seems inefficient. To better leverage the huge investments made into pretrained models, we develop the new "Assembly-of-Experts" (AoE) construction method to create capable child variants of existing Mixture-of-Experts parent models in linear time. Model weight tensors get interpolated individually, allowing to enhance or suppress semantic features of the parents. Varying the proportion of weights taken from the parent models, we observe some properties of the AoE child model changing gradually, while other behavioral traits emerge with a sharp transition. Surprisingly, nearly every generated model is functional and capable, which makes searching the model space straightforward. We construct the DeepSeek R1T "Chimera", a 671B open-weights hybrid model combining DeepSeek's V3-0324 and R1 model variants. The child inherits only the routed expert tensors of R1, but still achieves about R1-level intelligence. At the same time, it uses about 40% fewer output tokens, close to V3 speed. Constructed without any fine-tuning or distillation, the Chimera exhibits surprisingly compact, orderly reasoning compared to its parent models. The DeepSeek R1T Chimera model is available as open weights on [Hugging Face](https://huggingface.co/tngtech/DeepSeek-R1T-Chimera).
---

