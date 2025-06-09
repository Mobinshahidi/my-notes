---
title: book, chap 4
description: book, chap 4
---

# Chapter 4: Threads 🧵

## 1. Overview 🔍

A thread is the basic unit of CPU utilization, consisting of:
- Thread ID
- Program counter
- Register set
- Stack

Threads within the same process share:
- Code section
- Data section
- Other operating system resources (open files, signals, etc.)

### 1.1 Motivation for Using Threads

- Resource sharing: Threads share the resources of the process, making resource sharing more efficient
- Economy: Creating and managing threads is much less expensive than creating processes
- Responsiveness: Applications remain responsive even when parts are blocked or performing lengthy operations
- Scalability: Threads can take advantage of multiprocessor architectures, with each thread potentially running in parallel on a different processor

## 2. Multicore Programming 💻

Multicore or multiprocessor systems have become increasingly common, allowing concurrent programming to become even more important.

### 2.1 Programming Challenges

- Identifying tasks: Divide applications into separate, concurrent tasks
- Balance: Ensure tasks perform equal work of equal value
- Data splitting: Divide data for separate tasks
- Data dependency: Ensure tasks don't interfere with each other
- Testing and debugging: More difficult than single-threaded applications

### 2.2 Types of Parallelism

- Data parallelism: Same operation performed on different data items
- Task parallelism: Different operations performed on same or different data

### 2.3 Amdahl's Law

Amdahl's Law predicts the theoretical maximum speedup when using multiple processors:

- Formula: Speedup ≤ 1/[S + (1-S)/N]            
![[IMG-20250507171254161.png]]
  - S is the portion of the application that must be performed serially
  - N is the number of processing cores
  - (1-S) is the portion that can be parallelized

- Key implications:
  - If 75% of a program is parallelizable and we use 4 cores, maximum speedup is 2.29x
  - Limited by the serial portion of the program
  - Even with infinite processors, if just 10% of application is serial, maximum speedup is 10x
  - Emphasizes the importance of making as much of the application parallel as possible

## 3. Multithreading Models 🏗️

### 3.1 Many-to-One Model

- Maps many user-level threads to one kernel thread
- Thread management done by the thread library in user space
- Efficient thread management but limited concurrency
- If one thread makes a blocking system call, the entire process blocks
- Cannot take advantage of multiprocessing

### 3.2 One-to-One Model

- Maps each user thread to a kernel thread
- More concurrency than many-to-one model
- Allows multiple threads to run in parallel on multiprocessors
- Creating a user thread requires creating a corresponding kernel thread
- Overhead can burden system performance
- Examples: Windows, Linux, and later versions of UNIX

### 3.3 Many-to-Many Model

- Multiplexes many user-level threads to a smaller or equal number of kernel threads
- Developers can create as many user threads as necessary
- Kernel threads can run in parallel on a multiprocessor
- When a thread makes a blocking system call, the kernel can schedule another thread for execution
- Examples: Solaris prior to version 9

### 3.4 Two-level Model

- Similar to many-to-many but allows a user thread to be bound to a kernel thread
- Combines advantages of both many-to-many and one-to-one models

## 4. Thread Libraries 📚

Thread libraries provide programmers with an API for creating and managing threads.

### 4.1 Pthreads

- POSIX standard (IEEE 1003.1c) thread API
- Specification, not implementation
- Common in UNIX-like operating systems
- API for thread behavior, not how they are implemented

### 4.2 Windows Threads

- Windows thread library for the Windows OS
- Similar functionality to Pthreads
- Uses the one-to-one mapping model

### 4.3 Java Threads

- Thread creation through:
  - Extending Thread class
  - Implementing Runnable interface
- Managed by JVM, which uses host OS thread implementation

## 5. Implicit Threading 🔄

Implicit threading transfers the responsibility of creating and managing threads from application developers to compilers and run-time libraries.

### 5.1 Thread Pools

- Create a number of threads at process startup and place them in a pool
- When a server receives a request, it awakens a thread from the pool
- When the thread completes its service, it returns to the pool
- Benefits:
  - Faster service of requests
  - Limits the number of threads
  - Thread creation separated from task execution

### 5.2 OpenMP

- Set of compiler directives and an API for C, C++, and FORTRAN
- Identifies parallel regions as blocks of code that may run in parallel
- Example directive: `#pragma omp parallel`

### 5.3 Grand Central Dispatch (GCD)

- Apple technology for macOS and iOS operating systems
- Combination of language features, API, and runtime library
- Allows identification of parallel sections of code (blocks)
- Two types of dispatch queues:
  - Serial: Blocks removed in FIFO order, one block must complete before next starts
  - Concurrent: Multiple blocks can be removed at once

### 5.4 Intel Threading Building Blocks (TBB)

- C++ template library for parallel programming
- Abstracts thread management from the programmer
- Emphasizes task parallelism rather than data parallelism

## 6. Threading Issues 🚧

### 6.1 The fork() and exec() System Calls

- If one thread in a process calls fork(), does the new process duplicate all threads?
- Two options:
  - Duplicate all threads in the child process
  - Have child process contain only the thread that called fork()
- Different systems handle this differently
- If a thread calls exec(), the program specified in the parameter replaces the entire process

### 6.2 Signal Handling

- Signals are used in UNIX systems to notify a process that a particular event has occurred
- Options for delivering signals:
  - Deliver signal to the thread to which the signal applies
  - Deliver signal to every thread in the process
  - Deliver signal to certain threads in the process
  - Assign a specific thread to receive all signals for the process

### 6.3 Thread Cancellation

- Terminating a thread before it has completed
- Two general approaches:
  - Asynchronous cancellation: One thread immediately terminates the target thread
  - Deferred cancellation: Target thread periodically checks if it should terminate

### 6.4 Thread-Local Storage (TLS)

- Allows each thread to have its own copy of data
- Useful when you don't have control over the thread creation process
- Similar to static data, but specific to each thread

### 6.5 Scheduler Activations

- Both user and kernel threads implemented using an intermediate data structure called "lightweight process" (LWP)
- Communication mechanism between kernel and thread library
- "Upcalls" - kernel informs the thread library about certain events

## 7. Operating System Examples 🖥️

### 7.1 Windows Threads

- Implements the one-to-one mapping model
- Each thread contains:
  - Thread ID
  - Register set
  - Separate user and kernel stacks
  - Private data storage area
- Windows Vista introduced user-mode scheduling (UMS)

### 7.2 Linux Threads

- Implements POSIX Pthreads using the one-to-one model
- Uses clone() system call to create threads
- Treats all threads as processes that happen to share resources
- Thread creation treats threads more like processes
- No distinction between processes and threads at the kernel level

## Key Takeaways 🎯

- Threads provide an efficient way to improve application performance through parallelism.
- Threads represent a more lightweight alternative to processes for achieving concurrency.
- Different thread models (many-to-one, one-to-one, many-to-many) offer various tradeoffs between performance and concurrency.
- Thread libraries provide programmers with APIs for thread creation and management.
- Implicit threading abstracts thread management away from application developers.
- Thread management introduces complex issues like signal handling, thread cancellation, and thread-local storage.
- Modern operating systems implement threading in diverse ways, but typically favor the one-to-one mapping model.
