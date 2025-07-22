---
title: book, chap 7
description: book, chap 7
---


# Chapter 7: Synchronization Examples

## 7.1.1 Bounded-Buffer Problem (Producer-Consumer) 🔄
**Problem Description**:
- Producers generate data and place in buffer
- Consumers remove data from buffer
- Buffer has finite size
**Shared Data**:
```c
int n;
semaphore mutex = 1;    // mutual exclusion for buffer access
semaphore empty = n;    // count empty buffer slots
semaphore full = 0;     // count full buffer slots
```
**Producer Process**:
```c
do {
    // produce an item in next_produced
    wait(empty);
    wait(mutex);
    // add next_produced to buffer
    signal(mutex);
    signal(full);
} while (true);
```
**Consumer Process**:
```c
do {
    wait(full);
    wait(mutex);
    // remove an item from buffer to next_consumed
    signal(mutex);
    signal(empty);
    // consume the item in next_consumed
} while (true);
```
## 7.1.2 Readers-Writers Problem 📖
**Problem Description**:
- Multiple readers can access data simultaneously
- Only one writer can access data at a time
- No reader can access data while writer is writing
**Shared Data**:
```c
semaphore rw_mutex = 1;    // mutual exclusion for writers
semaphore mutex = 1;       // mutual exclusion for read_count
int read_count = 0;        // number of readers
```
**Writer Process**:
```c
do {
    wait(rw_mutex);
    // writing is performed
    signal(rw_mutex);
} while (true);
```
**Reader Process**:
```c
do {
    wait(mutex);
    read_count++;
    if (read_count == 1)
        wait(rw_mutex);
    signal(mutex);
    
    // reading is performed
    
    wait(mutex);
    read_count--;
    if (read_count == 0)
        signal(rw_mutex);
    signal(mutex);
} while (true);
```
**Variations**:
- **First readers-writers problem**: No reader waits unless writer has permission to use shared object
- **Second readers-writers problem**: Once writer is ready, it performs write ASAP
## 7.3 Dining-Philosophers Problem 🍽️
**Problem Description**:
- Five philosophers sit around circular table
- Each philosopher alternates between thinking and eating
- Five chopsticks, one between each pair of philosophers
- To eat, philosopher needs both adjacent chopsticks
**Semaphore Solution**:
```c
semaphore chopstick[5];
// Initialize all to 1

// Philosopher i
do {
    wait(chopstick[i]);
    wait(chopstick[(i + 1) % 5]);
    // eat
    signal(chopstick[i]);
    signal(chopstick[(i + 1) % 5]);
    // think
} while (true);
```
**Problems with Simple Solution**:
- **Deadlock**: All philosophers pick up left chopstick simultaneously
- **Starvation**: A philosopher may never get both chopsticks
**Solutions to Deadlock**:
1. Allow at most 4 philosophers at table simultaneously
2. Pick up chopsticks only if both are available (atomic operation)
3. Use asymmetric solution (odd philosophers pick up left first, even pick up right first)
**Monitor Solution**:
```c
monitor DiningPhilosophers {
    enum {THINKING, HUNGRY, EATING} state[5];
    condition self[5];
    
    void pickup(int i) {
        state[i] = HUNGRY;
        test(i);
        if (state[i] != EATING)
            self[i].wait();
    }
    
    void putdown(int i) {
        state[i] = THINKING;
        test((i + 4) % 5);    // test left neighbor
        test((i + 1) % 5);    // test right neighbor
    }
    
    void test(int i) {
        if ((state[(i + 4) % 5] != EATING) &&
            (state[i] == HUNGRY) &&
            (state[(i + 1) % 5] != EATING)) {
            state[i] = EATING;
            self[i].signal();
        }
    }
    
    initialization_code() {
        for (int i = 0; i < 5; i++)
            state[i] = THINKING;
    }
}
```
## 7.4 Synchronization within the Kernel ⚙️
## Windows Synchronization:
- **Interrupt masking**: For uniprocessor systems
- **Spinlocks**: For multiprocessor systems, short critical sections
- **Dispatcher objects**: For longer critical sections
    - Mutexes
    - Semaphores
    - Events
    - Timers
## Linux Synchronization:
- **Preemption disabling**: On uniprocessor systems
- **Memory barriers**: Ensure order of memory accesses
- **Spinlocks and Semaphores**: Standard synchronization tools
- **Reader-writer locks**: Multiple readers, single writer
**Linux Kernel Preemption**:
- Kernel is fully preemptive
- Task can be preempted when:
    - Returning from interrupt handler
    - Kernel code becomes preemptible again
    - Task explicitly calls schedule()
    - Task blocks
## Key Programming Concepts 💻

## POSIX API Example (Semaphores):
```c
##include <semaphore.h>

sem_t *sem;

// Create semaphore
sem = sem_open("SEM", O_CREAT, 0666, 1);

// Wait operation
sem_wait(sem);

// Signal operation  
sem_post(sem);

// Close semaphore
sem_close(sem);
```
## Java Synchronization Example:
```java
// Synchronized method
public synchronized void deposit(int amount) {
    balance += amount;
}

// Synchronized block
synchronized(this) {
    balance += amount;
}

// Using semaphores
import java.util.concurrent.Semaphore;

Semaphore sem = new Semaphore(1);
sem.acquire();  // wait
// critical section
sem.release();  // signal
```
## Summary and Key Takeaways 🎯
## Critical Concepts:
1. **Race conditions** occur when multiple processes access shared data concurrently
2. **Critical section problem** requires mutual exclusion, progress, and bounded waiting
3. **Peterson's solution** works theoretically but may fail on modern architectures
4. **Mutex locks** provide simple mutual exclusion with busy waiting
5. **Semaphores** offer more flexible synchronization with counting capability
6. **Monitors** provide high-level abstraction for synchronization
## Classic Problems:
- **Bounded Buffer**: Demonstrates producer-consumer synchronization
- **Readers-Writers**: Shows priority-based access control
- **Dining Philosophers**: Illustrates deadlock and starvation issues
## Implementation Considerations:
- **Busy waiting** vs **blocking**: Trade-off between CPU usage and context switching
- **Kernel synchronization**: Must handle interrupts and multiprocessor environments
- **API differences**: POSIX pthreads, Windows threads, Java synchronization
## Best Practices:
- Always acquire locks in same order to prevent deadlock
- Keep critical sections as short as possible
- Use appropriate synchronization primitive for the problem
- Consider starvation and fairness in design
- Test thoroughly in multiprocessor environments

