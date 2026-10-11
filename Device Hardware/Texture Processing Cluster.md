---
title: "What is a Texture Processing Cluster?"
aliases:
  - "TPC"
tags:
  - gpu-glossary
  - gpu-glossary/device-hardware
source: https://modal.com/gpu-glossary/device-hardware/texture-processing-cluster
---

# What is a Texture Processing Cluster? `TPC`

A Texture Processing Cluster (TPC) is a pair of adjacent [[Streaming Multiprocessor|Streaming Multiprocessors (SMs)]].

Before the Blackwell [[Streaming Multiprocessor Architecture|SM architecture]], TPCs were not mapped onto any level of the [[CUDA (Programming Model)|CUDA programming model]]'s [[Memory Hierarchy|memory hierarchy]] or [[Thread Hierarchy|thread hierarchy]].

The fifth-generation [[Tensor Core|Tensor Cores]] in the Blackwell [[Streaming Multiprocessor Architecture|SM architecture]] added the "CTA pair" level of the [[Parallel Thread eXecution|Parallel Thread eXecution (PTX)]] [[Thread Hierarchy|thread hierarchy]], which maps onto TPCs. Many `tcgen05` [[Parallel Thread eXecution|PTX]] instructions include a `.cta_group` field that can use a single [[Streaming Multiprocessor|SM]] (`.cta_group::1`) or a pair of [[Streaming Multiprocessor|SMs]] in a TPC (`::2`), which are mapped to `1SM` and `2SM` variants of [[Streaming ASSembler|Streaming Assembler (SASS)]] instructions like `MMA`.

---

← [[Streaming Multiprocessor Architecture]] · [[Graphics-GPU Processing Cluster|Graphics/GPU Processing Cluster]] →
