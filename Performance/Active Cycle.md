---
title: "What is an active cycle?"
tags:
  - gpu-glossary
  - gpu-glossary/perf
source: https://modal.com/gpu-glossary/perf/active-cycle
---

# What is an active cycle?

An active cycle is a clock cycle in which a [[Streaming Multiprocessor]] has at least one [[Warp Execution State|active warp]] resident. The [[Warp|warp]] may be [[Warp Execution State|eligible]] or [[Warp Execution State|stalled]].

![[terminal-cycles.svg]]

*All cycles depicted in this diagram are active cycles. Diagram inspired by the [_CUDA Techniques to Maximize Compute and Instruction Throughput_](https://www.nvidia.com/en-us/on-demand/session/gtc25-s72685/) talk at GTC 2025.*

---

← [[Warp Execution State]] · [[Occupancy]] →
