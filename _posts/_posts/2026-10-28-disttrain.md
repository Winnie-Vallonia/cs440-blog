---
layout: post
title: "DistTrain: Addressing Model and Data Heterogeneity with Disaggregated Training for Multimodal LLMs"
date: 2026-10-28
paper_authors: "Zili Zhang, Yinmin Zhong, Yimin Jiang, et al."
paper_venue: "SIGCOMM 2025"
paper_url: "https://doi.org/10.1145/3718958.3750472"
week: 6
tags: [distributed-training, multimodal-llm, pipeline-parallelism, disaggregation]
---

## Key Idea

Multimodal LLMs wrap an image encoder and generator around an LLM, but Megatron-LM trains all three with the same parallelism settings, so the cheap encoder and generator leave GPUs waiting on each other. DistTrain splits the model into three units with their own GPU counts, picked by a convex optimization that solves in under a second. It also moves preprocessing to separate CPU nodes, which lets it reorder samples within a batch to cut stragglers without changing the gradient sum.

## Critique

I liked that the ablations pull the two techniques apart and test frozen-module setups, not just one happy path. But the 2.2x headline is against a Megatron-LM the authors retrofitted themselves, with the encoder and generator sharing the LLM's settings, which makes the baseline easy to beat. The gain shrinks to 1.3x at 72B, reordering alone adds only 1.03 to 1.11x, and everything is images only (ViT and Stable Diffusion) on a private cluster.

## Connections

Megatron-LM's bubble math, (p-1)/m, assumes every pipeline stage takes equal time, and DistTrain is about what breaks when it doesn't. Next to last week's DCP post, which fixes the network underneath, DistTrain takes the RoCEv2 fabric as given and fixes how the work is spread across it.
