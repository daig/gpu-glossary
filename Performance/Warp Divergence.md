---
title: "What is warp divergence?"
tags:
  - gpu-glossary
  - gpu-glossary/perf
source: https://modal.com/gpu-glossary/perf/warp-divergence
---

# What is warp divergence?

Warp divergence occurs when threads within a [[Warp|warp]] take different execution paths due to control flow statements.

For example, consider this [[Kernel|kernel]]:

```cpp
__global__ void divergent_kernel(float* data, int n) {
    int idx = blockIdx.x * blockDim.x + threadIdx.x;
    if (idx < n) {
        if (data[idx] > 0.5f) {
		    // A
            data[idx] = data[idx] * 4.0f;
        } else {
		    // B
            data[idx] = data[idx] + 2.0f;
        }
        data[idx] = data[idx] * data[idx];
    }
}
```

When the [[Thread|threads]] within a [[Warp|warp]] encounter the data-dependent conditional, some [[Thread|threads]] must execute block A while others must execute block B, depending on the value at `data[idx]`. Because of this data-dependency and the structural constraints of the [[CUDA (Programming Model)|CUDA programming model]] and its implementation in the [[Parallel Thread eXecution|PTX machine model]], there is no way for a programmer or a compiler to avoid this split in control flow inside of the [[Warp|warp]].

Instead, the [[Warp Scheduler|warp scheduler]] must handle concurrent execution of these divergent code paths, which it achieves by "masking" some [[Thread|threads]] so that they don't execute the instruction. This is achieved using predicate [[Registers|registers]].

Let's examine the generated [[Streaming ASSembler|SASS]] ([Godbolt link](https://godbolt.org/z/EGWKb5oWr)) to understand the execution flow:

```nasm
LDG.E.SYS R4, [R2]                       // L1 load data[idx]
FSETP.GT.AND P0, PT, R4.reuse, 0.5, PT   // L2 set P0 to data[idx] > 0.5
FADD R0, R4, 2                           // L3 store 2 + data[idx] in R0
@P0 FMUL R0, R4, 4                       // L4 in some threads, store 4 * data[idx] in R0
FMUL R5, R0, R0                          // L5 store R0 * R0 in R5
STG.E.SYS [R2], R5                       // L6 store R5 in data[idx]
```

After loading the data into `R4` (`L1`), all 32 [[Thread|threads]] in the [[Warp|warp]] execute `FSETP.GT.AND` concurrently (`L2`), and each [[Thread|thread]] gets its own `P0` value based on the `data` value in `R4`. Then, we have a bit of [[NVIDIA CUDA Compiler Driver|compiler]] cleverness: in `L3` *all* [[Thread|threads]] execute the code in A, writing to `R0`. Only those for whom `P0` is true then execute the code in B (`L4`), over-writing the value written to `R0` in `L3`. On this instruction, the [[Warp|warp]] is said to be "divergent". On `L5`, all [[Thread|threads]] are back to executing the same code. Once the [[Warp Scheduler|warp scheduler]] brings them back into alignment by issuing the same instruction on the same clock cycle, the warp has "converged".

This is presumably more efficient than the naïve encoding of the branch into [[Streaming ASSembler|SASS]], which would instead predicate both lines `L3` and `L4` — "presumably" in that we can trust the [[NVIDIA CUDA Compiler Driver|compiler]] and in that, heuristically, we are trading use of cheap, plentiful [[CUDA Core]] computation for more expensive flow control. As often in GPU programming, it's better to waste compute (an unnecessary `FADD` for every execution of `L4`) than to add complexity, even if it's just a simple predication!

One reason compilers might aggressively avoid divergence is that in early (pre-Volta) GPUs, divergent [[Warp|warps]] were always fully serialized. While warp divergence still reduces efficiency, modern GPUs with independent thread scheduling don't necessarily experience the full serialization penalties.

---

← [[Streaming Multiprocessor Utilization]] · [[Scoreboard Stall]] →
