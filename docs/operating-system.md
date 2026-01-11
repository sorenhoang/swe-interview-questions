# Operating System Question

<details>
<summary>What is the difference between a process and a thread</summary>

* A process is an executing program with its own private virtual address space and OS-managed resources such as heap, stack, and file descriptors.

* Processes are isolated from each other, so a failure in one process usually does not affect others.

* A thread is the smallest unit of execution within a process.

  * Threads in the same process share memory and resources

  * Each thread has its own stack and program counter

* In terms of performance:

  * Thread context switching is cheaper than process switching since the address space does not change

  * Thread creation is faster than process creation

* In terms of safety:

  * Threads are more prone to race conditions and deadlocks without proper synchronization

  * Processes provide better fault isolation

</details>

<details>
<summary>Explain context switching and its cost.</summary>

Context switching is the process where the operating system saves the state of a running process or thread and restores the state of another one, allowing the CPU to switch execution.

During a context switch, the OS saves and restores:

* CPU registers

* Program counter

* Stack pointer

* CPU flags

* (For processes) memory address space and page tables

**Cost of context switching**

Context switching introduces several types of overhead:

* CPU overhead

  * Time spent saving and restoring execution state

  * No useful work is done during this time

* Cache impact

  * CPU caches and TLB may be invalidated or polluted

  * Leads to cache misses after the switch

* Memory overhead (process switch)

  * Process switches are more expensive than thread switches due to address space changes

* Scheduler overhead

  * The OS scheduler must select the next runnable entity

Cost comparison

* Thread context switching is cheaper than process context switching

* Excessive context switching can significantly reduce system throughput

In summary:
* Context switching enables multitasking, but too many context switches hurt performance.

</details>

<details>
<summary>What are the states of a process?</summary>

A process typically goes through the following states:

1. New: The process is being created and initialized.

2. Ready: The process is ready to run and waiting for CPU allocation.

3. Running: The process is currently executing on the CPU.

4. Waiting (Blocked): The process is waiting for an event, such as I/O completion.

5. Terminated (Exit): The process has finished execution or has been terminated.

State transitions

* New → Ready → Running

* Running → Waiting

* Waiting → Ready

* Running → Ready (preemption)

* Running → Terminated
</details>

<details>
<summary>How does CPU scheduling work?</summary>

CPU scheduling is the mechanism by which the operating system decides which process or thread gets the CPU at any given time.

How CPU scheduling works

* Ready processes or threads are placed in a ready queue.

* The scheduler selects one based on a scheduling algorithm.

* The dispatcher performs a context switch and assigns the CPU.

* Scheduling happens again when a process:

  * Finishes execution

  * Waits for I/O

  * Is preempted due to time slice expiration

Two main types of scheduling

* Non-preemptive scheduling: A process keeps the CPU until it terminates or blocks.

* Preemptive scheduling: The OS can interrupt and reassign the CPU to another process.

Goals of CPU scheduling

* Maximize CPU utilization

* Improve throughput

* Minimize waiting and response time

* Ensure fairness

In summary:
* CPU scheduling combines scheduling algorithms, context switching, and dispatcher logic to efficiently share CPU resources.
</details>