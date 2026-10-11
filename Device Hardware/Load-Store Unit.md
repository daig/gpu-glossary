---
title: "What is a Load/Store Unit?"
aliases:
  - "LSU"
  - "Load/Store Unit"
tags:
  - gpu-glossary
  - gpu-glossary/device-hardware
source: https://modal.com/gpu-glossary/device-hardware/load-store-unit
---

# What is a Load/Store Unit? `LSU`

The Load/Store Units (LSUs) dispatch requests to load or store data to the memory subsystems of the GPU.

![[terminal-gh100-sm.svg]]

*The internal architecture of an H100 SM. Load/Store Units are shown in pink, along with the [[Special Function Unit|Special Function Units]]. Modified from NVIDIA's [H100 white paper](https://modal-cdn.com/gpu-glossary/gtc22-whitepaper-hopper.pdf).*

Most importantly for [[CUDA (Software Platform)|CUDA programmers]], they interact directly with the [[Streaming Multiprocessor]]'s on-chip SRAM [[L1 Data Cache|L1 data cache]] and indirectly with the off-chip, on-device [[GPU RAM|global RAM]] that respectively implement the lowest and highest levels of the [[Memory Hierarchy|memory hierarchy]] in the [[CUDA (Programming Model)|CUDA programming model]].

---

← [[Special Function Unit]] · [[Warp Scheduler]] →
