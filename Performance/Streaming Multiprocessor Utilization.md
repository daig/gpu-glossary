---
title: "What is SM utilization?"
tags:
  - gpu-glossary
  - gpu-glossary/perf
source: https://modal.com/gpu-glossary/perf/streaming-multiprocessor-utilization
---

# What is SM utilization?

SM utilization measures the percentage of time that [[Streaming Multiprocessor|Streaming Multiprocessors (SMs)]] are executing instructions.

SM utilization is akin to the more familiar [kernel utilization](https://modal.com/blog/gpu-utilization-guide) reported by [`nvidia-smi`](<../Host Software/nvidia-smi.md>), but more fine-grained. Instead of reporting the fraction of time that a [[Kernel|kernel]] is executing anywhere on the GPU, it reports the fraction of time all [[Streaming Multiprocessor|SMs]] spend executing [[Kernel|kernels]]. If a [[Kernel|kernel]] uses only one [[Streaming Multiprocessor|SM]], e.g. because it only has one [[Thread Block|thread block]], then it will achieve 100% GPU utilization while it is active, but the SM utilization will be at most one over the number of [[Streaming Multiprocessor|SMs]] — under 1% in an H100 GPU.

[As with GPU utilization but unlike CPU utilization](https://modal.com/blog/gpu-utilization-guide), SM utilization should be high, even up to 100%.

But even though SM utilization is finer-grained than GPU utilization, it still isn't fine-grained enough to capture how well the GPU's compute resources are being used. If SM utilization is high, but performance is still inadequate, programmers should check [[Pipe Utilization|pipe utilization]], which measures how effectively each SM uses its internal functional units. High SM utilization with low [[Pipe Utilization|pipe utilization]] indicates that your [[Kernel|kernel]] is running on many SMs but not fully utilizing the computational resources within each one.

---

← [[Issue Efficiency]] · [[Warp Divergence]] →
