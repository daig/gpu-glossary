---
title: "What is latency hiding?"
tags:
  - gpu-glossary
  - gpu-glossary/perf
source: https://modal.com/gpu-glossary/perf/latency-hiding
---

# What is latency hiding?

Latency hiding is a strategy to mask long-latency operations by [[Little's Law|running many of them concurrently]].

Performant GPU programs hide latency by interleaving the execution of many [[Thread|threads]]. This allows programs to maintain high throughput despite long instruction latencies. When one [[Warp Execution State|warp stalls]] on a slow memory operation, the GPU immediately switches to execute instructions from another [[Warp Execution State|eligible warp]].

This keeps all execution units busy concurrently. While one [[Warp|warp]] uses [[Tensor Core|Tensor Cores]] for matrix multiplication, another might execute arithmetic on [[CUDA Core|CUDA Cores]] (say, [quantizing or dequantizing matrix multiplicands](https://arxiv.org/abs/2408.11743)), and a third could be fetching data through the [[Load-Store Unit|load/store units]].

Concretely, consider the following simple instruction sequence in [[Streaming ASSembler|Streaming Assembler]].

```nasm
LDG.E.SYS R1, [R0]        // memory load, 400 cycles
IMUL R2, R1, 0xBEEF       // integer multiply, 6 cycles
IADD R4, R2, 0xAFFE       // integer add, 4 cycles
IMUL R6, R4, 0x1337       // integer multiply, 6 cycles
```

Executed sequentially, this would take 416 cycles to complete. We can hide this latency by operating concurrently. If we assume we can issue one instruction every cycle, then, by [[Little's Law]], if we run 416 concurrent [[Thread|threads]], we can still finish the sequence once per cycle (on average), hiding the latency of memory from consumers of the data in `R6`.

Note that [[Thread|threads]] are not the unit of instruction issuance, [[Warp|warps]] are. Each [[Warp|warp]] contains 32 [[Thread|threads]], and so our fragment requires 416 ÷ 32 = 13 [[Warp|warps]]. When successfully hiding latency, the GPU's scheduling system maintains this many [[Warp|warps]] in flight, switching between them whenever one stalls, ensuring the execution units never idle while waiting for slow operations to complete.

For a deep dive into latency hiding on pre-[[Tensor Core]] GPUs, see [Vasily Volkov's PhD thesis](https://www2.eecs.berkeley.edu/Pubs/TechRpts/2016/EECS-2016-143.pdf).

---

← [[Arithmetic Bandwidth]] · [[Warp Execution State]] →
