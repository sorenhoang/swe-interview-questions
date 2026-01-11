# Computer Architecture Question

<details>
<summary>What is the difference between CPU and GPU?</summary>

* CPU is designed for general-purpose computing: few powerful cores, complex control logic, optimized for low latency and sequential / branch-heavy tasks.

* GPU is designed for massive parallelism: thousands of simpler cores, optimized for high throughput and data-parallel workloads like graphics, ML, and matrix operations.

* In short: CPU = latency & control, GPU = throughput & parallelism.
</details>

<details>
<summary>Explain the Von Neumann architecture</summary>

* It is a computer architecture where instructions and data share the same memory and bus.

* The CPU follows a fetch–decode–execute cycle, reading instructions and data from the same address space.

* Main drawback is the Von Neumann bottleneck, where instruction and data access compete for bandwidth.

</details>

<details>
<summary>What is instruction pipelining</summary>

**Instruction pipelining:**

  * A technique that divides instruction execution into multiple stages (**Fetch, Decode, Execute, Memory, Write-back**).

  * Multiple instructions are processed in parallel at different stages of the pipeline.

  * It improves throughput, but not the latency of a single instruction.

</details>

<details>
<summary>Pipeline hazards and how to resolve them</summary>

Pipeline hazards and solutions:

  * Data hazards: caused by data dependencies
  → solved by forwarding, stalling, or instruction reordering.

  * Control hazards: caused by branches
  → solved by branch prediction or pipeline flushing.

  * Structural hazards: caused by resource conflicts
  → solved by resource duplication or better pipeline design.

</details>

<details>
<summary>What is cache memory and why is it important?</summary>

  * Cache memory is a small, high-speed memory located close to the CPU that stores frequently accessed data and instructions.
  * It is important because there is a large speed gap between the CPU and main memory, and accessing RAM directly would significantly slow down execution.
  * By exploiting temporal and spatial locality, cache reduces average memory access time and greatly improves overall system performance.

</details>