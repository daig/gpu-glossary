---
title: "What is issue efficiency?"
tags:
  - gpu-glossary
  - gpu-glossary/perf
source: https://modal.com/gpu-glossary/perf/issue-efficiency
---

# What is issue efficiency?

Issue efficiency measures how effectively the [[Warp Scheduler|warp scheduler]] keeps execution pipes busy by issuing instructions from [[Warp Execution State|eligible warps]].

![[terminal-cycles.svg]]

*Of the four clock cycles in this diagram, instructions were issued on three, for an issue efficiency of 75%. Diagram inspired by the [_CUDA Techniques to Maximize Compute and Instruction Throughput_](https://www.nvidia.com/en-us/on-demand/session/gtc25-s72685/) talk at GTC 2025.*

An issue efficiency of 100% means every [[Warp Scheduler|scheduler]] issued an instruction on every cycle, indicating at least one [[Warp Execution State|eligible warp]] on each cycle. Values below 100 % signal that, during some cycles, all [[Warp Execution State|active warps]] were [[Warp Execution State|stalled]] - waiting on data, resources, or dependencies - so the [[Warp Scheduler|scheduler]] sat idle and overall instruction throughput fell.

---

← [[Peak Rate]] · [[Streaming Multiprocessor Utilization]] →
