---
title: "What is a CUDA Core?"
tags:
  - gpu-glossary
  - gpu-glossary/device-hardware
source: https://modal.com/gpu-glossary/device-hardware/cuda-core
---

# What is a CUDA Core?

The CUDA Cores are GPU [[Core|cores]] that execute scalar arithmetic instructions.

![[terminal-gh100-sm.svg]]

*The internal architecture of an H100 SM. The CUDA Cores and Tensor Cores are depicted in green. Note the larger size and lower number of Tensor Cores. Modified from NVIDIA's [H100 white paper](https://modal-cdn.com/gpu-glossary/gtc22-whitepaper-hopper.pdf).*

They are to be contrasted with the [[Tensor Core|Tensor Cores]], which execute matrix operations.

Unlike CPU cores, instructions issued to CUDA Cores are not generally independently scheduled. Instead, groups of cores are issued the same instruction simultaneously by the [[Warp Scheduler]] but apply that instruction to different [[Registers|registers]]. Commonly, these groups are of size 32, the size of a [[Warp|warp]], but for contemporary GPUs groups can contain as little as one thread, at a cost to performance.

The term "CUDA Core" is slightly slippery: in different [[Streaming Multiprocessor Architecture|Streaming Multiprocessor architectures]] CUDA Cores can consist of different units -- a different mixture of 32 bit integer and 32 bit and 64 bit floating point units. They are perhaps best thought of in contrast to early GPUs, which contained a variety of much more specialized compute units mapped onto shader pipelines (see [[CUDA (Device Architecture)|CUDA Device Architecture]]).

So, for example, the [H100 whitepaper](https://resources.nvidia.com/en-us-hopper-architecture/nvidia-h100-tensor-c) indicates that an H100 GPU's [[Streaming Multiprocessor|Streaming Multiprocessors (SMs)]] each have 128 "FP32 CUDA Cores", which accurately counts the number of 32 bit floating point units but is double the number of 32 bit integer or 64 bit floating point units (as evidenced by the diagram above). For estimating performance, it's best to look directly at the number of hardware units for a given operation.

---

← [[Warp Scheduler]] · [[Tensor Core]] →
