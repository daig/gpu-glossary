---
title: "What is a GPU Core?"
tags:
  - gpu-glossary
  - gpu-glossary/device-hardware
source: https://modal.com/gpu-glossary/device-hardware/core
---

# What is a GPU Core?

The cores are the primary compute units that make up the [[Streaming Multiprocessor|Streaming Multiprocessors (SMs)]].

![[terminal-gh100-sm.svg]]

*The internal architecture of an H100 GPU's Streaming Multiprocessors. CUDA and Tensor Cores are shown in green. Modified from NVIDIA's [H100 white paper](https://modal-cdn.com/gpu-glossary/gtc22-whitepaper-hopper.pdf).*

Examples of GPU core types include [[CUDA Core|CUDA Cores]] and [[Tensor Core|Tensor Cores]].

Though GPU cores are comparable to CPU cores in that they are the component that effects actual computations, this analogy can be quite misleading. Instead, it is perhaps more helpful to take the viewpoint of the [quantitative computer architect](https://archive.org/details/computerarchitectureaquantitativeapproach6thedition) and think of them as "pipes" into which data goes in and out of which transformed data is returned. These pipes are associated in turn with specific [[Streaming ASSembler|instructions]] from the hardware's perspective and with different fundamental affordances of throughput from the programmers' (e.g. floating point matrix multiplication arithmetic throughput in the case of the [[Tensor Core|Tensor Cores]]).

The [[Streaming Multiprocessor|SMs]] are closer to being the equivalent of CPU cores, in that they have [[Register File|register memory]] to store information, cores to transform it, and an [[Warp Scheduler|instruction scheduler]] to specify and command transformations.

---

← [[Streaming Multiprocessor]] · [[Special Function Unit]] →
