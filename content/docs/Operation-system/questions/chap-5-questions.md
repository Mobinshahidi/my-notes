---
title: chap 5 questions
description: chap 5 questions
---


## ✅ Chapter 5 – Practice Questions

### 🟢 EASY

1. What is the purpose of **CPU scheduling**?
2. What is **CPU burst time**?
3. What does **turnaround time** mean?
4. Define **waiting time**.
5. What is **response time**?
6. What is the difference between **preemptive** and **non-preemptive** scheduling?
7. Name three common **CPU scheduling algorithms**.
8. Which algorithm uses a **time quantum**?
9. Which algorithm gives priority to the **shortest job**?
10. Why is **scheduling needed** in multiprogramming systems?

---

### 🟡 MEDIUM

1. Describe the trade-offs between **FCFS** and **Round Robin**.
2. Why can **SJF** be difficult to implement in practice?
3. How does **aging** solve the starvation problem?
4. What is a **convoy effect**, and in which algorithm does it happen?
5. Explain how **priority scheduling** can lead to starvation.
6. Describe how **context switching** affects CPU scheduling.
7. How is **time quantum** size important in **Round Robin**?
8. What is the difference between **throughput** and **CPU utilization**?
9. Explain how a **multilevel queue** works.
10. What is the goal of a **multilevel feedback queue**?

---

### 🔴 HARD

1. Compare **SJF**, **SRTF**, and **Priority** scheduling in terms of waiting time and complexity.
2. Explain how **process burst prediction** can be done in SJF.
3. What makes **Round Robin** fair but inefficient in some cases?
4. Describe the internal working of a **feedback queue** with an example.
5. How does the **scheduler decide** which process runs next?
6. Why can frequent **context switches** hurt performance?
7. Explain the difference between **real-time scheduling** and general-purpose scheduling.
8. What happens if a high-priority process enters the ready queue during Round Robin?
9. Describe the role of **dispatch latency**.
10. In what scenarios is **First-Come, First-Served** the best choice?

---

## 📘 Detailed Answers

### 🟢 EASY

1. **CPU scheduling** selects which process gets the CPU next when multiple are ready.
2. **CPU burst** = the time a process uses the CPU before doing I/O or waiting.
3. **Turnaround time** = time from process submission to completion.
4. **Waiting time** = total time a process spends in the **ready queue**.
5. **Response time** = time from request submission to the **first response**.
6. * **Preemptive**: CPU can be taken from a process
   * **Non-preemptive**: Process keeps CPU until done or blocks
7. FCFS, SJF, Round Robin, Priority, Multilevel Queue
8. **Round Robin**
9. **Shortest Job First (SJF)**
10. Because multiple processes are in memory; CPU must be shared among them.

---

### 🟡 MEDIUM

1. * **FCFS** is simple but can lead to **long wait** (convoy effect)
   * **RR** gives fairness but overhead increases if time quantum is small
2. SJF needs knowledge of **future burst time**, which is hard to predict accurately.
3. **Aging** increases the priority of waiting processes to prevent starvation.
4. **Convoy effect**: one long process delays many short ones. Happens in FCFS.
5. If low-priority processes never get scheduled, they **starve**. Aging fixes this.
6. Switching between processes takes **time & resources** → reduces performance if too frequent.
7. * Too small → too many context switches
   * Too big → behaves like FCFS (less responsive)
8. * **Throughput** = # of processes completed per time
   * **CPU Utilization** = % of time CPU is active
9. Processes are divided by type (interactive, system, batch) into **separate queues**, each with its own scheduling.
10. Multilevel Feedback Queues adjust process priority over time → **dynamic behavior**.

---

### 🔴 HARD

1. * **SJF**: Optimal waiting time, but needs burst estimate
   * **SRTF**: Preemptive SJF, even more efficient, even harder to predict
   * **Priority**: Custom control, can starve low-priority processes
2. Use **exponential averaging**:
   `τ(n+1) = α * T(n) + (1 - α) * τ(n)`
   Predicts next burst from past behavior.
3. Fair, but too small quantum = many switches (overhead), too large = long wait for others.
4. Example:

   * New processes start in Q0 (high priority, small quantum)
   * If they use full quantum → move to Q1 (lower priority, bigger quantum)
   * If still CPU-heavy → move to Q2
     → Encourages **I/O-bound** processes and penalizes **CPU-bound** ones.
5. Scheduler uses algorithm rules (e.g., shortest burst, highest priority) to pick next from **ready queue**.
6. Each switch adds **CPU overhead** → bad for systems with many short tasks.
7. * **Real-time**: strict timing, deadlines must be met
   * **General-purpose**: optimized for fairness, responsiveness, not deadlines
8. High-priority process **preempts** current task depending on the algorithm.
9. **Dispatch latency** = time to stop one process and start another.
10. FCFS is best when tasks are **same length** and **order matters**, like print queues or batch jobs.
