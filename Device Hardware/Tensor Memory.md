---
title: "What is Tensor Memory?"
tags:
  - gpu-glossary
  - gpu-glossary/device-hardware
source: https://modal.com/gpu-glossary/device-hardware/tensor-memory
---

# What is Tensor Memory?

Tensor Memory is a specialized memory in the [[Streaming Multiprocessor|Streaming Multiprocessor (SM)]] of certain GPUs, like the [B200](https://modal.com/blog/introducing-b200-h200), for storing the inputs and outputs of [[Tensor Core|Tensor Cores]].

Tensor Memory access is highly restricted. Data must be moved collectively by four [[Warp|warps]] in a [[Warpgroup|warpgroup]], and they can move memory only in specific patterns between Tensor Memory and [[Registers|registers]], write [[Shared Memory|shared memory]] to Tensor Memory, or issue matrix-multiply-accumulate (MMA) instructions to [[Tensor Core|Tensor Cores]] that use Tensor Memory for specific operands. So much for a [[CUDA (Device Architecture)|"compute-unified" device architecture]]!

Specifically, for a `tcgen05.mma` [[Parallel Thread eXecution]] instruction computing `D += A @ B` to use Tensor Memory, the "accumulator" matrix `D` *must* be in Tensor Memory, the left-hand matrix `A` *may* be in Tensor Memory or [[Shared Memory|shared memory]], and the right-hand matrix B *must* be in [[Shared Memory|shared memory]], not Tensor Memory. This is complex, but not arbitrary -- accumulators are accessed more frequently during matmuls than are the tiles, so they benefit more from specialized hardware, e.g. from shorter, simpler wiring between the [[Tensor Core|Tensor Cores]] and the Tensor Memory. Note that none of the matrices are in the [[Registers|registers]].

Beware: Tensor Memory is not directly related to the [[Tensor Memory Accelerator]], which instead loads into the [[L1 Data Cache|L1 data cache]]. Roughly speaking, data is moved from that cache into Tensor Memory only as a result of a [[Tensor Core]] operation and then is explicitly moved out for post-processing, e.g. the non-linearity after a matrix multiplication in a neural network.

For details on tensor memory and patterns for its use in matrix multiplications, see the [*Programming Blackwell Tensor Cores with CUTLASS* talk from GTC 2025](https://www.nvidia.com/en-us/on-demand/session/gtc25-s72720/).

---

← [[L1 Data Cache]] · [[GPU RAM]] →
