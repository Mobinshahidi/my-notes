---
title: chap-3-questions
description: chap-3-questions
---


## ✅ **Chapter 3 – Practice Questions**

### 🟢 Easy

1. What is a **process**?
2. List three components of a process in memory.
3. What is a **PCB (Process Control Block)**?
4. What are the five typical **process states**?
5. What is the difference between **program** and **process**?
6. What’s stored in the **stack** of a process?
7. Which system call is used to create a process in UNIX?
8. Define **ready queue** and **I/O queue**.
9. What is **context switch**?
10. What happens when a process is terminated?

---

### 🟡 Medium

1. What is the difference between **parent** and **child** processes?
2. Explain **zombie** and **orphan** processes.
3. What’s the purpose of `fork()` and `exec()` in process creation?
4. Describe how a **context switch** affects CPU performance.
5. What is the role of **PID** and **PPID**?
6. Describe the role of the **long-term**, **short-term**, and **medium-term** schedulers.
7. What happens during a **context switch**? List key steps.
8. How does the OS **maintain process control** using the PCB?
9. Why is process scheduling necessary in modern OS?
10. What does **wait()** do in process synchronization?

---

### 🔴 Hard

1. Describe the full lifecycle of a process using a diagram or flow.
2. Explain the **process creation and execution** path in UNIX.
3. How does the OS ensure **fairness** between CPU-bound and I/O-bound processes?
4. How does **multitasking** rely on **context switching**?
5. Explain how **Interprocess Communication (IPC)** is used and the difference between shared memory and message passing.
6. What are the pros/cons of **blocking vs non-blocking communication**?
7. How does the OS avoid **race conditions** in process communication?
8. Discuss the role of **signals** in UNIX process control.
9. What are **direct vs indirect communication** models in IPC?
10. Explain **process hierarchy** and how process groups work.

---

## 📘 **Detailed Answers**

### 🟢 Easy

1. A **process** is a program in execution, with its own memory and resources.
2. Code (text), data (variables), stack (function calls), heap (dynamic memory).
3. **PCB** stores process info like state, PID, CPU registers, scheduling info.
4. New → Ready → Running → Waiting → Terminated
5. A **program** is a passive file; a **process** is the active execution of that file.
6. The stack holds **function calls**, **return addresses**, and **local variables**.
7. `fork()` in UNIX duplicates the current process.
8. **Ready queue**: waiting for CPU
   **I/O queue**: waiting for I/O device
9. **Context switch** = saving the current process state and restoring another's.
10. Its resources are reclaimed, and its status is stored for parent (if any) to read.

---

### 🟡 Medium

1. **Parent** spawns the child using `fork()`; **child** inherits resources and executes separately.
2. **Zombie**: finished process, not yet cleaned by parent.
   **Orphan**: child still running after parent exits.
3. `fork()` copies the process; `exec()` replaces the process’s memory with a new program.
4. It causes **overhead**, since saving/restoring CPU state takes time.
5. **PID** identifies a process. **PPID** links to its parent.
6. * **Long-term**: selects jobs for admission
   * **Short-term**: picks ready processes for CPU
   * **Medium-term**: swaps processes in/out of memory
7. * Save current process's PCB state
   * Load new process's PCB state
   * Update CPU registers and program counter
8. The **PCB** acts as the OS's way to track and manage each process.
9. The CPU must be shared fairly among all active processes → scheduler does this.
10. `wait()` blocks a parent until the child finishes → prevents zombie buildup.

---

### 🔴 Hard

1. **Process Lifecycle**:
   New → Ready → Running → (Waiting ↔ Ready) → Terminated
   (Context switch happens between Ready ↔ Running)

2. * Shell runs `fork()` to duplicate itself
   * In child: `exec()` replaces memory with new program
   * Parent waits or continues

3. **Fairness** via scheduling algorithms like **multilevel queues**, which separate CPU-bound (compute-heavy) and I/O-bound (fast I/O) processes to ensure balance.

4. **Multitasking** means running multiple apps at once.
   OS switches between them using **context switching**, giving illusion of parallelism.

5. * **IPC** allows processes to cooperate or communicate.
   * **Shared Memory** is fast but complex to sync.
   * **Message Passing** is simpler but slower due to system call overhead.

6. * **Blocking** waits for the message → simpler, easier sync
   * **Non-blocking** continues immediately → faster but harder to manage

7. OS uses **locks**, **semaphores**, or **monitors** to protect shared resources and avoid race conditions.

8. **Signals** are used to interrupt or notify processes (e.g., `SIGKILL`, `SIGCHLD`).

9. * **Direct**: sender & receiver name each other
   * **Indirect**: use a mailbox/port abstraction to send messages

10. * Parent can spawn multiple children = **process tree**
    * Process groups allow managing multiple processes together (e.g., job control in UNIX)
