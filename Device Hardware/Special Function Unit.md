---
title: "What is a Special Function Unit?"
aliases:
  - "SFU"
tags:
  - gpu-glossary
  - gpu-glossary/device-hardware
source: https://modal.com/gpu-glossary/device-hardware/special-function-unit
---

# What is a Special Function Unit? `SFU`

The Special Function Units (SFUs) in [[Streaming Multiprocessor|Streaming Multiprocessors (SMs)]] accelerate certain arithmetic operations.

![[terminal-gh100-sm.svg]]

*The internal architecture of an H100 SM. Special Function Units are shown in maroon, along with the [[Load-Store Unit|Load/Store Units]]. Modified from NVIDIA's [H100 white paper](https://modal-cdn.com/gpu-glossary/gtc22-whitepaper-hopper.pdf).*

Notable for neural network workloads are transcendental mathematical operations, like `exp`, `sin`, and `cos`.

The [[Streaming ASSembler|Streaming Assembler (SASS)]] instructions associated with the SFUs generally begin with `MUFU`: `MUFU.SQRT`, `MUFU.EX2`. See [this Godbolt link](https://godbolt.org/z/WGh3rPe83) for sample assembly using the `MUFU.EX2` instruction to implement the `expf` intrinsic in [[CUDA C++ (programming language)|CUDA C++]].

---

← [[Core]] · [[Load-Store Unit|Load/Store Unit]] →
