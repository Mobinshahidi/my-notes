---
title: chap-1-questions
description: chap-1-questions
---

## ✅ Chapter 1 – Practice Questions

### 🟢 EASY (10 Questions)

1. What is an operating system?
2. Name four components of a computer system.
3. What is the function of the kernel?
4. Define the term "resource allocator" in the context of OS.
5. What does the term "control program" mean in OS terminology?
6. Name one volatile and one non-volatile memory type.
7. What does a device controller do?
8. What is the purpose of the bootstrap program?
9. What is the role of a system call?
10. What is a trap in operating systems?

---

### 🟡 MEDIUM (10 Questions)

1. How does an operating system handle multiple I/O requests at the same time?
2. Explain the difference between a system program and an application program.
3. What is the difference between multiprogramming and multitasking?
4. How do interrupts improve CPU efficiency?
5. What is the purpose of a memory controller?
6. Describe the difference between symmetric and asymmetric multiprocessing.
7. How do timers help the OS control processes?
8. Describe the function of the memory hierarchy in terms of performance.
9. Why is a cache needed in modern systems?
10. What is the role of a device driver in I/O communication?

---

### 🔴 HARD (10 Questions)

1. Explain the steps taken from compiling a program to running it in memory.
2. How does the OS ensure security when switching between user and kernel modes?
3. Describe three reasons why a binary compiled on one OS may not run on another.
4. What’s the difference between monolithic, microkernel, and modular OS structures?
5. Why are system calls preferred over allowing direct hardware access by applications?
6. Explain how virtualization can improve system utilization and flexibility.
7. In a NUMA system, what challenges arise with memory access speed?
8. What are the consequences of having no protection mechanism between processes?
9. Describe the role of the OS in a cluster computing environment.
10. How does the OS ensure that the cache remains coherent across multiple cores?

## 🟢 EASY – Detailed Answers

1. **What is an operating system?**
   An OS is system software that manages hardware and software resources and provides services for programs.

2. **Name four components of a computer system.**
   Hardware, Operating System, Application Programs, Users.

3. **What is the function of the kernel?**
   It's the core of the OS, always running, managing memory, processes, I/O, and hardware.

4. **Define "resource allocator" in OS.**
   The OS manages and allocates CPU time, memory, and I/O resources among users and applications.

5. **What does "control program" mean in OS terminology?**
   A program that controls execution to prevent errors and improper use of the system.

6. **Name one volatile and one non-volatile memory type.**
   Volatile: RAM; Non-volatile: SSD/HDD/EEPROM.

7. **What does a device controller do?**
   It's hardware that manages communication between a device and the system's bus/memory.

8. **What is the purpose of the bootstrap program?**
   It initializes the system when the computer is powered on and loads the OS into memory.

9. **What is the role of a system call?**
   It's the interface between user applications and OS services (e.g., file access, I/O).

10. **What is a trap in operating systems?**
    A software-generated interrupt, triggered by errors or specific instructions (e.g., divide by zero).

---

## 🟡 MEDIUM – Detailed Answers

1. **How does an OS handle multiple I/O requests at once?**
   Through **interrupts**, **device queues**, and sometimes **DMA** to parallelize and manage efficiently.

2. **Difference between system program and application program?**
   System: supports OS (e.g., compiler, shell). Application: user-facing (e.g., browser, games).

3. **Multiprogramming vs Multitasking?**
   Multiprogramming: multiple processes in memory.
   Multitasking: fast switching between tasks, giving the illusion of parallelism.

4. **How do interrupts improve CPU efficiency?**
   They let the CPU work on other tasks instead of waiting for I/O to finish.

5. **What is the purpose of a memory controller?**
   It manages access to RAM and ensures orderly read/write operations between devices and memory.

6. **Symmetric vs Asymmetric Multiprocessing?**
   SMP: all processors are equal.
   AMP: one master processor controls others (less flexible).

7. **How do timers help control processes?**
   They interrupt processes after a time slice, enabling multitasking and avoiding infinite loops.

8. **Function of memory hierarchy in performance?**
   Faster, smaller memory (like cache) sits closer to CPU; large, slow storage (like HDD) stores long-term data.

9. **Why is cache needed?**
   To bridge speed gap between CPU and main memory, reducing latency and improving performance.

10. **Role of device driver in I/O?**
    A software layer that translates OS commands into hardware-specific signals for the device controller.

---

## 🔴 HARD – Detailed Answers

1. **Steps from compiling to execution:**
   Source code → Compiler → Object files → Linker → Executable → Loader → Process created → CPU executes.

2. **How does OS protect using user/kernel modes?**
   By running user programs in restricted user mode; kernel mode has full privileges. Switching is controlled via traps/system calls.

3. **Why binary from one OS may not run on another:**

   * Different CPU architecture (e.g., ARM vs x86)
   * Different binary format (ELF vs PE)
   * Different system calls/APIs
   * Linked libraries missing
   * OS-specific dependencies

4. **OS Structures:**

   * **Monolithic**: All functionality in one large kernel (e.g., Linux).
   * **Microkernel**: Only essentials in kernel, others in user space (e.g., QNX).
   * **Modular**: Kernel can load/unload parts (e.g., Linux modules).

5. **Why use system calls instead of direct hardware access?**
   System calls ensure controlled, secure, and consistent access to hardware, reducing risks and improving stability.

6. **Virtualization benefits:**
   OS can simulate multiple machines → better hardware utilization, isolation, and flexibility (e.g., VMs, containers).

7. **NUMA challenges:**
   Accessing remote memory is slower than local memory. Requires smart memory allocation and process placement.

8. **Consequences of no memory protection:**

   * A faulty/malicious process can overwrite others
   * System crashes
   * Security breaches

9. **Role of OS in cluster computing:**
   Coordinates resource sharing, job distribution, fault tolerance, and communication between nodes.

10. **Cache coherence across cores:**
    OS (and hardware protocols like MESI) must ensure that changes in one core’s cache are reflected in others or flushed to memory.
