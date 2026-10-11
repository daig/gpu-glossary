---
title: "What is GPU RAM?"
tags:
  - gpu-glossary
  - gpu-glossary/device-hardware
source: https://modal.com/gpu-glossary/device-hardware/gpu-ram
---

# What is GPU RAM?

![[terminal-hbm-schematic.svg]]

*In high-performance data center GPUs like the H100, RAM is located on a die directly next to the processor's. Adapted from the Wikipedia page for [high-bandwidth memory](https://en.wikipedia.org/wiki/High_Bandwidth_Memory).*

The bottom-level memory of the GPU is a large (many megabytes to gigabytes) memory store that is addressable by all of the GPU's [[Streaming Multiprocessor|Streaming Multiprocessors (SMs)]].

It is also known as GPU RAM (random access memory) or video RAM (VRAM). It uses Dynamic RAM (DRAM) cells, which are slower but smaller than the Static RAM (SRAM) used in [[Register File|registers]] and [[L1 Data Cache|cache memory]]. For details on DRAM and SRAM, we recommend Ulrich Drepper's 2007 article ["What Every Programmer Should Know About Memory"](https://people.freebsd.org/~lstewart/articles/cpumemory.pdf).

It is generally not on the same die as the [[Streaming Multiprocessor|SMs]], though in the latest data center-grade GPUs like the H100, it is located on a shared [interposer](https://en.wikipedia.org/wiki/Interposer) for decreased latency and increased [[Memory Bandwidth|bandwidth]]. These GPUs use [High-Bandwidth Memory (HBM)](https://en.wikipedia.org/wiki/High_Bandwidth_Memory) technology, rather than the more familiar Double Data Rate (DDR) memory in consumer GPUs and CPUs.

RAM is used to implement the [[Global Memory|global memory]] of the [[CUDA (Programming Model)|CUDA programming model]] and to store [[Registers|register]] data that spills from the [[Register File|register file]].

An H100 can store 80 GiB (687,194,767,360 bits) in its RAM.

---

← [[Tensor Memory]] · [[Device Software]] →
