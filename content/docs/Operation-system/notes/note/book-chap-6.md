---
title: book, chap 6
description: book, chap 6
---

# Chapter 6: Synchronization Tools

## 6.1 Background 🌟
**Race Condition**: A situation where several processes access and manipulate the same data concurrently, and the outcome depends on the particular order of access.
**Critical Section Problem**: Design a protocol that processes can use to cooperate. Each process has a critical section where it may change common variables, update tables, write files, etc.
## Structure of a Process:
```
do {
    entry section
        critical section
    exit section
        remainder section
} while (true);
```
## Requirements for Critical Section Solution:
1. **Mutual Exclusion**: If process Pi is executing in its critical section, no other process can execute in their critical sections
2. **Progress**: If no process is executing in its critical section and some processes wish to enter, only processes not executing in remainder section can participate in decision
3. **Bounded Waiting**: There exists a bound on number of times other processes are allowed to enter critical sections after a process has made request
## 6.2 Peterson's Solution 🔧
Peterson's solution is a classic software-based solution to the critical-section problem for two processes.
**Assumptions**:
- LOAD and STORE machine-language instructions are atomic
- Two processes share two variables:
    - `int turn`: indicates whose turn it is to enter critical section
    - `boolean flag[2]`: indicates if a process is ready to enter critical section
**Algorithm for Process Pi**:
```c
do {
    flag[i] = true;
    turn = j;
    while (flag[j] && turn == j);
        critical section
    flag[i] = false;
        remainder section
} while (true);
```
**Properties**:
- ✅ Satisfies all three requirements for critical section solution
- ❌ Not guaranteed to work on modern computer architectures due to instruction reordering
## 6.5 Mutex Locks 🔒
**Mutex** (mutual exclusion) locks are the simplest synchronization tool.
**Basic Operations**:
- `acquire()`: acquire the lock
- `release()`: release the lock
**Implementation**:
```c
acquire() {
    while (!available)
        ; /* busy wait */
    available = false;
}

release() {
    available = true;
}
```
**Using Mutex**:
```c
do {
    acquire lock
        critical section
    release lock
        remainder section
} while (true);
```
**Characteristics**:
- **Busy waiting**: Process continuously loops while waiting
- **Spinlock**: A mutex lock using busy waiting
- **Advantages**: No context switch required
- **Disadvantages**: Wastes CPU cycles
## 6.6 Semaphores 🚦
A **semaphore** S is an integer variable accessed through two standard atomic operations:
- `wait(S)` (also called P or down)
- `signal(S)` (also called V or up)
## 6.6.1 Semaphore Usage
**Binary Semaphore** (Mutex):
- Range between 0 and 1
- Similar to mutex locks
**Counting Semaphore**:
- Range over unrestricted domain
- Used to control access to finite number of resources
**Classic Implementation**:
```c
wait(S) {
    while (S <= 0)
        ; // busy wait
    S--;
}

signal(S) {
    S++;
}
```
## 6.6.2 Semaphore Implementation without Busy Waiting
**Problem with busy waiting**: Wastes CPU cycles
**Solution**: Block waiting processes
**Modified Semaphore Structure**:
```c
typedef struct {
    int value;
    struct process *list;
} semaphore;
```
**Operations**:
```c
wait(semaphore *S) {
    S->value--;
    if (S->value < 0) {
        add this process to S->list;
        block();
    }
}

signal(semaphore *S) {
    S->value++;
    if (S->value <= 0) {
        remove a process P from S->list;
        wakeup(P);
    }
}
```
**Key Points**:
- When semaphore value is negative, its absolute value indicates number of waiting processes
- No busy waiting in critical section implementation
- May still have busy waiting in interrupt handlers
## 6.7 Monitors 👁️
A **monitor** is a high-level abstraction providing convenient and effective mechanism for process synchronization.
## Monitor Characteristics:
- Only one process may be active within the monitor at a time
- Programmer doesn't need to code synchronization constraints explicitly
- Monitor ensures mutual exclusion
## Condition Variables:
```c
condition x, y;
```
**Operations on condition variables**:
- `x.wait()`: Process invoking this operation is suspended
- `x.signal()`: Resumes exactly one suspended process
## Monitor Implementation Using Semaphores:
```c
semaphore mutex; // initially = 1
semaphore next; // initially = 0
int next_count = 0;
```
**Monitor Entry**:
```c
wait(mutex);
...
body of F
...
if (next_count > 0)
    signal(next);
else
    signal(mutex);
```

