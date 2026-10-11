---
title: "What is warp execution state?"
tags:
  - gpu-glossary
  - gpu-glossary/perf
source: https://modal.com/gpu-glossary/perf/warp-execution-state
---

# What is warp execution state?

The state of the [[Warp|warps]] running a [[Kernel|kernel]] is described with a number of non-exclusive adjectives: active, stalled, eligible, and selected.

![[terminal-cycles.svg]]

*Warp execution states are indicated by color. Diagram inspired by the [_CUDA Techniques to Maximize Compute and Instruction Throughput_](https://www.nvidia.com/en-us/on-demand/session/gtc25-s72685/) talk at GTC 2025.*

A [[Warp|warp]] is considered *active* from the time its [[Thread|threads]] begin executing to the time when all [[Thread|threads]] in the [[Warp|warp]] have exited from the [[Kernel|kernel]]. Active [[Warp|warps]] form the pool from which [[Warp Scheduler|warp schedulers]] select candidates for instruction issue each cycle (i.e. to be put in one of the issue slots).

The maximum number of active [[Warp|warps]] per [[Streaming Multiprocessor|Streaming Multiprocessor (SM)]] varies by [[Streaming Multiprocessor Architecture|architecture]] and is listed in [NVIDIA's documentation](https://docs.nvidia.com/cuda/cuda-c-programming-guide/index.html?highlight=compute%2520capability#compute-capabilities) for [[Compute Capability]]. For instance, on an H100 SXM GPU with [[Compute Capability]] 9.0, there can be up to 64 active [[Warp|warps]] per [[Streaming Multiprocessor|SM]] (2048 threads). Note that active [[Warp|warps]] are not necessarily executing instructions. There are active [[Warp|warps]] in all but one slot+cycle in the diagram above — a high [[Occupancy|occupancy]].

An *eligible* [[Warp|warp]] is an active [[Warp|warp]] that is ready to issue its next instruction. For a [[Warp|warp]] to be eligible, the following must be true:

- the next instruction has been fetched,
- the required execution unit is available,
- all instruction dependencies have been resolved, and
- no synchronization barriers block execution.

Eligible [[Warp|warps]] represent the immediate candidates for instruction issue by the [[Warp Scheduler|warp scheduler]]. Eligible [[Warp|warps]] appear on all cycles but cycle n + 2 in the diagram above. Having no eligible [[Warp|warps]] on many cycles can be bad for performance, especially if you are primarily using lower latency arithmetic units like [[CUDA Core|CUDA Cores]].

A *stalled* [[Warp|warp]] is an active [[Warp|warp]] that cannot issue its next instruction due to unresolved dependencies or resource conflicts. [[Warp|Warps]] become stalled for various reasons including:

- execution dependencies, i.e. they must wait for results from previous arithmetic instructions,
- memory dependencies, i.e. they must wait for results from previous memory operations,
- pipeline conflicts, i.e. the execution resources are currently occupied.

When warps are stalled on accesses to shared memory or on long-running arithmetic instructions, they are said to be stalled on the "short scoreboard". When warps are stalled on accesses to GPU RAM, they are said to be stalled on the "long scoreboard". Both types of stalls are known as [[Scoreboard Stall|scoreboard stalls]].

Stalled [[Warp|warps]] appear in multiple slots in each cycle in the diagram above. Stalled [[Warp|warps]] are not inherently bad — a large collection of concurrently stalled [[Warp|warps]] might be necessary to [[Latency Hiding|hide latency]] from long-running instructions, like memory loads or [[Tensor Core]] instructions like `HMMA`, which [can run for dozens of cycles](https://arxiv.org/abs/2206.02874).

A *selected* [[Warp|warp]] is an eligible [[Warp|warp]] chosen by the [[Warp Scheduler|warp scheduler]] to receive an instruction during the current cycle. Each cycle, [[Warp Scheduler|warp schedulers]] look at their pool of eligible [[Warp|warps]], select one if there are any, and issue it an instruction. There is a selected [[Warp|warp]] on each cycle with an eligible [[Warp|warp]]. The fraction of [[Active Cycle|active cycles]] on which a [[Warp|warp]] is selected and an instruction is issued is the [[Issue Efficiency|issue efficiency]].

---

← [[Latency Hiding]] · [[Active Cycle]] →
