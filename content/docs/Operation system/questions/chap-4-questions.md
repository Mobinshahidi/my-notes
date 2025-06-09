---
title: chap 4 questions
description: chap 4 questions
---

## ✅ Chapter 4 – Practice Questions

### 🟢 EASY

1. What is a **thread**?
2. What do **threads** share within a process?
3. What is the main difference between a **thread** and a **process**?
4. Name three benefits of using threads.
5. What is **parallelism**?
6. What is **concurrency**?
7. Do threads have their own stack?
8. What part of memory is **not shared** between threads?
9. What is a **thread library**?
10. Give one example of a thread library.

---

### 🟡 MEDIUM

1. Explain the concept of **data parallelism** vs **task parallelism**.
2. What is a **user-level thread**?
3. What is a **kernel-level thread**?
4. Compare **user-level vs kernel-level** threads.
5. What is the **many-to-one** threading model?
6. Describe the **one-to-one** threading model.
7. What is the **many-to-many** model?
8. What are the benefits of the many-to-many model?
9. In Java, how are threads managed?
10. What is a **thread pool** and why is it useful?

---

### 🔴 HARD

1. Why can user-level threads be faster but also limited?
2. What is a **thread context switch**, and how is it different from a process context switch?
3. Describe a scenario where **multithreading improves performance**.
4. Explain how **shared resources** between threads can lead to problems.
5. What is a **race condition**?
6. How does the OS handle **thread scheduling**?
7. Why does the many-to-one model not benefit from multi-core systems?
8. What is the danger of not synchronizing threads properly?
9. Explain the difference between **blocking and non-blocking** thread behavior.
10. Why does multithreaded programming require extra caution from the developer?

---

## 📘 Detailed Answers

### 🟢 EASY

1. A **thread** is the smallest unit of execution within a process.
2. Threads share the same **code**, **data**, and **open files** of a process.
3. A thread is **lighter** than a process; threads share memory, processes are isolated.
4. Benefits:

   * Faster context switch
   * Resource sharing
   * Responsiveness (especially for UI or I/O-heavy tasks)
5. **Parallelism**: tasks executed **simultaneously** on different cores.
6. **Concurrency**: tasks executed **out of order or interleaved**, giving illusion of simultaneity.
7. Yes — each thread has its own **stack** (function calls, local variables).
8. **Stack and registers** are not shared between threads.
9. A **thread library** is an API that lets you create, manage, and synchronize threads.
10. Examples: **Pthreads** (POSIX), **Windows threads**, **Java threads**

---

### 🟡 MEDIUM

1. * **Data parallelism**: same task on different parts of data
   * **Task parallelism**: different tasks run in parallel
2. **User-level threads** are managed by a **thread library** in user space (OS doesn’t see them).
3. **Kernel-level threads** are managed directly by the **OS**.
4. * **User-level**: fast, no kernel involvement
   * **Kernel-level**: more control, OS-managed, slower context switch
5. **Many-to-one**: many user threads → **one kernel thread** → only one runs at a time.
6. **One-to-one**: each user thread = **one kernel thread** → parallelism possible, more overhead.
7. **Many-to-many**: user threads mapped to **a pool** of kernel threads dynamically.
8. Flexibility, scalability, allows true parallelism without oversubscribing the kernel.
9. Java threads are managed by the **JVM** and mapped to native threads (usually kernel-level).
10. A **thread pool** is a set of pre-created threads reused for tasks, reducing thread creation overhead.

---

### 🔴 HARD

1. * **Faster** because no kernel interaction
   * **Limited**: if one thread blocks (e.g., for I/O), all others block too
2. * **Thread context switch** = save/restore registers, stack pointer, program counter for threads
   * **Process switch** = all above + MMU (memory) + PCB changes → more overhead
3. Example: A server handling many client requests → each request handled by a thread → faster and more scalable.
4. Threads share memory → if they access the same variable **without locks**, it can cause **unexpected behavior**.
5. **Race condition**: outcome depends on timing of threads accessing shared data → can cause inconsistent results.
6. OS uses scheduling algorithms (like **priority**, **round robin**) to manage thread execution in kernel-level threading.
7. In **many-to-one**, all threads are bound to one kernel thread → no use of multiple cores.
8. It can lead to **deadlocks**, **race conditions**, or **inconsistent data**.
9. * **Blocking**: thread waits until operation finishes
   * **Non-blocking**: thread continues without waiting → more complex logic
10. Because shared memory and asynchronous behavior make it harder to predict all possible execution orders.
