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

* 
* Maximize CPU utilization

* Improve throughput

* Minimize waiting and response time

* Ensure fairness

In summary:
* CPU scheduling combines scheduling algorithms, context switching, and dispatcher logic to efficiently share CPU resources.
</details>

<details>
<summary>Why do they say that Thread is a lightweight process?</summary>

A thread is called a lightweight process because it requires fewer system resources than a process while still being an independent unit of execution.

Key reasons:

* Resource sharing

  * Threads within the same process share the address space, heap, and file descriptors

  * Processes have fully isolated resources

* Lower creation cost

  * Creating a thread is faster and cheaper than creating a process

  * No need to allocate a new address space

* Cheaper context switching

  * Thread context switches do not require changing the address space

  * This makes them significantly cheaper than process switches

* Efficient communication

  * Threads communicate via shared memory

  * Processes usually rely on IPC mechanisms, which are more expensive

Trade-off

* Because threads share memory, they are more prone to race conditions and synchronization issues
</details>

<details>
<summary>Can 2 different processes access or change data of each other address space?</summary>

Yes. Although process that have isolate address space. but they can access or change data of each other by some mechanisms provided by the operating system. Some common methods include:
* Inter-Process Communication (IPC):

  * Mechanisms like pipes, message queues, and sockets allow processes to exchange data.
* Shared Memory:

  * The OS can allocate a shared memory segment that multiple processes can map into their address spaces.
* Message Passing:
  * Processes can send and receive messages to share data without directly accessing each other's memory.
* Debugging and Tracing Tools:

  * Some OS-level debugging tools allow one process to inspect or modify another process's memory for debugging purposes.

</details>

<details>
<summary>What is child-process? How to create a child-process?</summary>

* Child-process is a process created by another process (the parent process) using system calls provided by the operating system (usually fork() in Unix-like systems).
  * Each child-process has only one parent process, but a parent process can have multiple child-processes.
  * Child-processes inherit certain attributes from their parent(such as environment variables, open file descriptors, etc.), but they have their own separate memory space.
  * if a parent process terminates before its child-processes, the child-processes are adopted by the init process (PID 1) in Unix-like systems.
* To Create a child-process:
  * In Unix-like systems, the fork() system call is used to create a new child-process. When a process calls fork(), the operating system creates a duplicate of the calling process.
  * The fork() call returns twice: once in the parent process (returning the child's PID) and once in the child-process (returning 0).
</details>

<details>
<summary>What is copy on write (COW), Dirty COW?</summary>

* Copy-On-Write (COW) is an optimization strategy used in computer programming and operating systems to efficiently manage memory. When multiple processes share the same data, COW allows them to share the same physical memory pages until one of the processes attempts to modify the data. At that point, a separate copy of the data is created for the modifying process, ensuring that changes do not affect the original data or other processes.
* Dirty COW is a specific vulnerability (CVE-2016-5195) that exploits the Copy-On-Write mechanism in the Linux kernel. It allows an unprivileged user to gain write access to read-only memory mappings, potentially leading to privilege escalation. The vulnerability arises from a race condition in the way the kernel handles COW, allowing an attacker to manipulate memory in a way that bypasses normal access controls.
</details>