---
title: "What is a Warpgroup?"
tags:
  - gpu-glossary
  - gpu-glossary/device-software
source: https://modal.com/gpu-glossary/device-software/warpgroup
---

# What is a Warpgroup?

A warpgroup is a set of four contiguous [[Warp|warps]] such that the warp-rank of the first warp is a multiple of 4.

Upon dispatching a warpgroup-level instruction, we coordinate 128 [[Thread|threads]] -- 4 warps per warpgroup × 32 threads per warp. Operating at a larger granularity removes the need for explicit inter-warp synchronization and allows work to be performed on larger problem sizes per instruction, especially larger matrix multiplications. Larger matrix multiplications more readily saturate the massive [[Arithmetic Bandwidth|arithmetic bandwidth]] of the [[Tensor Core|Tensor Cores]] of recent data center GPUs.

Warpgroups were introduced in NVIDIA's Hopper [[Streaming Multiprocessor Architecture|Streaming Multiprocessor architecture]], where they are used to support warpgroup-level matrix multiplication, like `wgmma.mma_async`. See [this blog post from Colfax](https://research.colfax-intl.com/cutlass-tutorial-wgmma-hopper/) for a deep dive. Warpgroups feature prominently in the organization of pipeline components of high-performance Hopper and Blackwell [[Kernel|kernels]], like [Flash Attention 4](https://modal.com/blog/reverse-engineer-flash-attention-4).

In [[Parallel Thread eXecution|Parallel Thread Execution (PTX)]] IR, the warp-rank of a warp is:

```cpp
int linearIdx = (%tid.x + %tid.y * %ntid.x  + %tid.z * %ntid.x * %ntid.y);
int warpRank = linearIdx / 32;
```

where `tid` is the thread index, accessed via special PTX [[Registers|registers]].

So the valid warpgroups for an 8-warp dispatch are:

- **Warpgroup 0**: warp-ranks 0, 1, 2, and 3
- **Warpgroup 1**: warp-ranks 4, 5, 6, and 7.

To our knowledge, the purpose of the warp-rank alignment restriction is not documented. But [[Streaming Multiprocessor|Streaming Multiprocessors]] for recent data center GPUs appear to contain four (unnamed) subunits, each with their own [[Warp Scheduler]] and Tensor Core.

---

← [[Warp]] · [[Cooperative Thread Array]] →
