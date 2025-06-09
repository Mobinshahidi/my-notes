---
title: main concept of os
description: main concept of os
---

## 🌍 Main Concept: What is an Operating System?

An **Operating System (OS)** is a software layer that manages **hardware resources** and provides **services** to applications. It's the **interface between user and hardware**.

* Acts as:

  * **Resource Allocator**: Manages CPU, memory, I/O devices, etc.
  * **Control Program**: Prevents misuse of the system and manages process execution.
  * **User Interface Provider**: GUI, CLI, APIs.

---

## 🧠 Understanding the System Structure

### 🔧 Hardware → 🔄 OS → 📱 Application → 👤 User

### OS Components:

* **Kernel**: Core program always running.
* **System Programs**: Provide functionalities like compilers, loaders.
* **Application Programs**: Word processors, browsers, etc.
* **Middleware** (in mobile systems): Additional layer for platform support.

---

## ⚙️ Program Execution Flow (from Source Code to Running Program)

### 1. **Source Code** (.c, .cpp, .java)

Written by developer.

### 2. **Compiler**

Converts source code → **object files** (.o) → relocatable format.

### 3. **Linker**

Combines object files + libraries → **binary executable**.

### 4. **Loader**

Loads the binary into memory and prepares it for CPU execution.

* **Static Linking**: Everything linked at compile time.
* **Dynamic Linking**: Some libraries (DLLs, .so) linked during runtime.

### 5. **Execution by CPU**

* OS assigns the process a memory space and creates **PCB** (Process Control Block).
* CPU fetches instructions → decodes → executes.

---

## 🔄 Processes (Chapter 3)

### What is a Process?

* A **process** = program in execution with its own:

  * Code (text)
  * Data (variables)
  * Stack (function calls)
  * Heap (dynamic memory)

### Managed via **PCB**:

* PID, state, registers, program counter, memory limits, etc.

### Process Lifecycle:

1. **New** → 2. **Ready** → 3. **Running** → 4. **Waiting** (I/O) → 5. **Terminated**

### Creation & Termination:

* `fork()`, `exec()` in UNIX, `CreateProcess()` in Windows
* Parent & Child relationship
* Zombie, Orphan processes

---

## 🔗 Inter-Process Communication (IPC)

### Two Models:

* **Shared Memory**: Fast, user-managed
* **Message Passing**: Kernel managed, easier in distributed systems

### Communication Forms:

* Direct vs Indirect
* Blocking vs Non-blocking
* Synchronous vs Asynchronous
* Buffering: None, bounded, unbounded

---

## 🧵 Threads (Chapter 4)

### Thread vs Process:

* **Threads share** code, data, files
* **Processes are isolated**

### Each thread has:

* Own PC, registers, stack

### Benefits:

* Better performance
* Efficient concurrency

### Models:

| Model        | Description                     |
| ------------ | ------------------------------- |
| Many-to-One  | Many user → 1 kernel thread     |
| One-to-One   | 1 user ↔ 1 kernel thread        |
| Many-to-Many | Many user → Many kernel threads |

### Libraries:

* **Pthreads** (POSIX)
* **Windows Threads**
* **Java Threads**

---

## 🧠 CPU Scheduling (Chapter 5)

### Why Scheduling?

* Many processes want CPU → OS must choose wisely

### Types:

* **Non-preemptive**: Current process runs till done
* **Preemptive**: Can switch mid-execution

### Scheduling Criteria:

| Metric          | Goal     |
| --------------- | -------- |
| CPU Utilization | Maximize |
| Throughput      | Maximize |
| Waiting Time    | Minimize |
| Turnaround Time | Minimize |
| Response Time   | Minimize |

### Algorithms:

| Name                | Type           | Notes                                    |
| ------------------- | -------------- | ---------------------------------------- |
| FCFS                | Non-preemptive | Simple, can cause convoy effect          |
| SJF / SRTF          | Both           | Optimal wait, hard to predict burst time |
| Round Robin         | Preemptive     | Time quantum based, fair                 |
| Priority Scheduling | Both           | May cause starvation → fix with aging    |
| Multilevel Queue    | Mixed          | Separate queues by priority              |
| Feedback Queue      | Dynamic        | Process moves across queues              |

---

## 🧩 How All These Concepts Connect

* **User runs program** → OS uses **loader** to create **process**
* OS creates **PCB**, schedules process using **CPU scheduler**
* OS may spawn **threads** for concurrency
* Threads/processes may communicate using **IPC**
* OS handles context switches between them
* All interactions use **system calls**

### Bonus:

* **OS must protect** memory and resources → uses **dual-mode** + **timer**
* Uses **caches** and **DMA** for fast I/O
* Uses **interrupts** and **device drivers** for hardware interaction
