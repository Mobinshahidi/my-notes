---
title: book, chap 5
description: book, chap 5
---


# Chapter 5: CPU Scheduling ⚡

## 5.1 Basic Concepts 🎯

### 5.1.1 CPU-I/O Burst Cycle 🔄

Process execution consists of a cycle of CPU execution and I/O wait:
- **CPU Burst**: Period when process is executing instructions on the CPU
- **I/O Burst**: Period when process is waiting for I/O completion
- **Pattern**: Process execution begins with CPU burst, followed by I/O burst, then CPU burst, and so on

#### Characteristics of CPU Bursts
- **Distribution**: Large number of short CPU bursts and small number of long CPU bursts
- **Typical Pattern**: Many processes have short CPU bursts (1-8 milliseconds)
- **CPU-bound processes**: Few long CPU bursts
- **I/O-bound processes**: Many short CPU bursts
- **Histogram Shape**: Exponential or hyperexponential curve with high frequency of short bursts

### 5.1.2 CPU Scheduler 🎛️

**Definition**: The CPU scheduler (short-term scheduler) selects which process in the ready queue should be allocated the CPU next.

#### When CPU Scheduling Occurs
CPU scheduling decisions take place when a process:
1. **Switches from running to waiting state** (e.g., I/O request, wait for child termination)
2. **Switches from running to ready state** (e.g., interrupt occurs)
3. **Switches from waiting to ready state** (e.g., I/O completion)
4. **Terminates**

#### Types of Scheduling
- **Nonpreemptive (Cooperative) Scheduling**: 
  - Scheduling occurs only under circumstances 1 and 4
  - Process keeps CPU until it releases it voluntarily
  - Used in Windows 3.x and early Macintosh
  
- **Preemptive Scheduling**:
  - Scheduling can occur under all four circumstances
  - Process can be forcibly removed from CPU
  - Used in modern operating systems
  - **Advantage**: Better response time and fairness
  - **Disadvantage**: Requires special hardware (timer interrupt) and careful design

#### Preemption Considerations
**Race Conditions**: 
- Can occur when preemption happens during kernel mode execution
- **Solution**: Wait for system call completion or I/O block before context switch
- **Alternative**: Use kernel synchronization primitives

**Interrupt Handling**:
- Interrupts can occur at any time
- Kernel must be designed to handle interrupts properly during critical sections

### 5.1.3 Dispatcher 🚀

**Definition**: The dispatcher gives control of the CPU to the process selected by the CPU scheduler.

#### Dispatcher Functions
1. **Context switching**: Save state of current process, load state of new process
2. **Mode switching**: Switch from kernel mode to user mode
3. **Jump to proper location**: Resume execution at the correct instruction in user program

#### Dispatch Latency
- **Definition**: Time taken by dispatcher to stop one process and start another
- **Components**:
  - Time to save context of current process
  - Time to load context of new process
  - Time for mode switch and instruction jump
- **Goal**: Minimize dispatch latency for better system responsiveness
- **Typical Range**: Few microseconds to milliseconds

## 5.2 Scheduling Criteria 📊

### 5.2.1 Performance Metrics 📈

Different scheduling algorithms optimize for different criteria:

#### CPU Utilization 💹
- **Definition**: Percentage of time the CPU is busy executing processes
- **Goal**: Maximize CPU utilization
- **Range**: 0% to 100%
- **Real Systems**: 40% (lightly loaded) to 90% (heavily loaded)
- **Formula**: CPU Utilization = (Total CPU Busy Time / Total Time) × 100%

#### Throughput 🏃‍♂️
- **Definition**: Number of processes completed per unit time
- **Goal**: Maximize throughput
- **Measurement Units**: Processes per second, processes per minute, processes per hour
- **Factors**: Depends on process length and system load
- **Example**: 10 processes/second for short processes vs 1 process/hour for long processes

#### Turnaround Time ⏱️
- **Definition**: Total time from process submission to completion
- **Formula**: Turnaround Time = Completion Time - Arrival Time
- **Components**: 
  - Waiting time in ready queue
  - CPU execution time
  - I/O waiting time
- **Goal**: Minimize average turnaround time
- **User Perspective**: Most important metric for batch systems

#### Waiting Time ⏳
- **Definition**: Total time process spends waiting in the ready queue
- **Formula**: Sum of all time periods spent in ready queue
- **Excludes**: CPU execution time and I/O waiting time
- **Goal**: Minimize average waiting time
- **Impact**: Directly affects user satisfaction

#### Response Time 🎯
- **Definition**: Time from request submission until first response is produced
- **Formula**: Response Time = Time of First Response - Arrival Time
- **Difference from Turnaround**: Measures time to begin responding, not time to complete
- **Goal**: Minimize average response time
- **Critical for**: Interactive and real-time systems
- **User Experience**: Affects perceived system responsiveness

### 5.2.2 Optimization Goals 🎯

#### General Principles
- **CPU Utilization**: Maximize (keep CPU as busy as possible)
- **Throughput**: Maximize (complete more processes per unit time)
- **Turnaround Time**: Minimize (reduce total completion time)
- **Waiting Time**: Minimize (reduce time spent waiting)
- **Response Time**: Minimize (improve interactive experience)

#### Trade-offs
- **Throughput vs Response Time**: Optimizing for high throughput may increase response time
- **Fairness vs Efficiency**: Fair scheduling may reduce overall system efficiency
- **Average vs Maximum**: Minimizing average response time may increase maximum response time

#### System-Specific Optimization
- **Batch Systems**: Emphasize throughput and turnaround time
- **Interactive Systems**: Emphasize response time
- **Real-time Systems**: Emphasize meeting deadlines
- **Server Systems**: Balance between throughput and response time

## 5.3 Scheduling Algorithms 📋

### 5.3.1 First-Come, First-Served (FCFS) Scheduling 🚶‍♂️

**Principle**: Processes are executed in the order they arrive in the ready queue.

#### Algorithm Description
- **Implementation**: Using FIFO (First-In, First-Out) queue
- **Process Selection**: Always select the process at the head of the queue
- **Preemption**: Nonpreemptive algorithm
- **Simplicity**: Easiest scheduling algorithm to understand and implement

#### FCFS Example
**Processes with CPU burst times**:
- P₁: 24ms, P₂: 3ms, P₃: 3ms
- Arrival order: P₁, P₂, P₃

**Gantt Chart**:
```
P₁        P₂   P₃
0    24   27   30
```

**Performance Metrics**:
- **Waiting Times**: P₁ = 0ms, P₂ = 24ms, P₃ = 27ms
- **Average Waiting Time**: (0 + 24 + 27)/3 = 17ms
- **Turnaround Times**: P₁ = 24ms, P₂ = 27ms, P₃ = 30ms
- **Average Turnaround Time**: (24 + 27 + 30)/3 = 27ms

#### FCFS with Different Arrival Order
**Same processes, different order**: P₂, P₃, P₁

**Gantt Chart**:
```
P₂   P₃   P₁
0    3    6    30
```

**Performance Metrics**:
- **Waiting Times**: P₁ = 6ms, P₂ = 0ms, P₃ = 3ms
- **Average Waiting Time**: (6 + 0 + 3)/3 = 3ms
- **Improvement**: 17ms → 3ms (significant improvement)

#### Convoy Effect 🚛
- **Definition**: Short processes get stuck behind long processes
- **Problem**: Poor performance when long CPU burst process arrives first
- **Impact**: Reduces CPU and device utilization
- **Example**: All processes wait for one long process to complete
- **Real-world Analogy**: Traffic jam caused by slow vehicle in front

#### FCFS Characteristics
**Advantages**:
- Simple to implement and understand
- Fair in the sense of first-come, first-served
- No starvation (every process eventually gets CPU)
- Low overhead

**Disadvantages**:
- Poor average waiting time performance
- Convoy effect problem
- Not suitable for interactive systems
- Inefficient for systems with mixed workload (CPU-bound and I/O-bound processes)

**Best Suited For**:
- Batch systems where fairness is more important than efficiency
- Systems with similar process characteristics
- Simple embedded systems

### 5.3.2 Shortest-Job-First (SJF) Scheduling ⚡

**Principle**: Select the process with the smallest CPU burst time for execution.

#### Algorithm Description
- **Selection Criteria**: Choose process with minimum CPU burst time
- **Optimality**: Provably optimal for minimizing average waiting time
- **Tie Breaking**: Use FCFS for processes with equal burst times
- **Implementation Challenge**: Requires knowledge of CPU burst times

#### SJF Example
**Processes with CPU burst times**:
- P₁: 6ms, P₂: 8ms, P₃: 7ms, P₄: 3ms

**Execution Order**: P₄ → P₁ → P₃ → P₂

**Gantt Chart**:
```
P₄   P₁      P₃       P₂
0    3       9        16       24
```

**Performance Metrics**:
- **Waiting Times**: P₁ = 3ms, P₂ = 16ms, P₃ = 9ms, P₄ = 0ms
- **Average Waiting Time**: (3 + 16 + 9 + 0)/4 = 7ms
- **Comparison with FCFS**: Would be (0 + 6 + 14 + 21)/4 = 10.25ms

#### Preemptive SJF (Shortest-Remaining-Time-First - SRTF) 🏃‍♀️

**Principle**: If a new process arrives with CPU burst time less than remaining time of current executing process, preempt the current process.

#### SRTF Example
**Processes with arrival times and burst times**:
- P₁: Arrival = 0ms, Burst = 8ms
- P₂: Arrival = 1ms, Burst = 4ms  
- P₃: Arrival = 2ms, Burst = 9ms
- P₄: Arrival = 3ms, Burst = 5ms

**Execution Timeline**:
- **0-1ms**: P₁ runs (remaining = 7ms)
- **1ms**: P₂ arrives (4ms < 7ms), preempt P₁
- **1-2ms**: P₂ runs (remaining = 3ms)
- **2ms**: P₃ arrives (9ms > 3ms), continue P₂
- **2-3ms**: P₂ runs (remaining = 2ms)
- **3ms**: P₄ arrives (5ms > 2ms), continue P₂
- **3-5ms**: P₂ completes
- **5-10ms**: P₄ runs (5ms < 7ms)
- **10-17ms**: P₁ completes
- **17-26ms**: P₃ completes

**Gantt Chart**:
```
P₁  P₂    P₂  P₄     P₁       P₃
0   1     2   3      5        10       17       26
```

**Performance Metrics**:
- **Waiting Times**: P₁ = (0) + (10-1) = 9ms, P₂ = (1-1) = 0ms, P₃ = (17-2) = 15ms, P₄ = (5-3) = 2ms
- **Average Waiting Time**: (9 + 0 + 15 + 2)/4 = 6.5ms

#### Estimating CPU Burst Time 📊

Since exact CPU burst times are unknown, they must be estimated:

**Exponential Averaging Formula**:
τₙ₊₁ = α × tₙ + (1-α) × τₙ

Where:
- **τₙ₊₁**: Predicted CPU burst time for next execution
- **tₙ**: Actual CPU burst time of nth execution  
- **τₙ**: Predicted CPU burst time for nth execution
- **α**: Smoothing parameter (0 ≤ α ≤ 1)

**Parameter α Effects**:
- **α = 0**: τₙ₊₁ = τₙ (only history matters, recent behavior ignored)
- **α = 1**: τₙ₊₁ = tₙ (only most recent behavior matters)
- **Typical α**: 0.5 (balances recent and historical data)

**Expansion of Formula**:
τₙ₊₁ = α × tₙ + (1-α) × α × tₙ₋₁ + (1-α)² × α × tₙ₋₂ + ... + (1-α)ⁿ × τ₀

**Interpretation**: More recent CPU bursts have higher weights in prediction

#### SJF Characteristics

**Advantages**:
- **Optimal**: Minimizes average waiting time
- **Good throughput**: Short jobs complete quickly
- **Efficient**: Reduces convoy effect

**Disadvantages**:
- **Starvation**: Long processes may never execute
- **Unpredictable**: CPU burst time estimation is difficult
- **Overhead**: Preemptive version requires context switching
- **Unfair**: Favors short processes over long ones

**Applications**:
- Batch systems with known job characteristics
- Systems where process behavior can be predicted
- Situations where minimizing average waiting time is crucial

### 5.3.3 Round-Robin (RR) Scheduling 🎡

**Principle**: Each process gets a small unit of CPU time (time quantum), after which it's preempted and moved to the end of the ready queue.

#### Algorithm Description
- **Time Quantum**: Fixed time slice (typically 10-100 milliseconds)
- **Queue Structure**: Circular FIFO queue
- **Preemption**: Occurs when time quantum expires
- **Fair Sharing**: Each process gets equal CPU time allocation
- **Implementation**: Uses timer interrupt to enforce time quantum

#### Round-Robin Example
**Processes with CPU burst times**:
- P₁: 24ms, P₂: 3ms, P₃: 3ms
- **Time Quantum**: 4ms

**Execution Timeline**:
1. **0-4ms**: P₁ runs (remaining = 20ms)
2. **4-7ms**: P₂ runs (remaining = 0ms, completes)
3. **7-10ms**: P₃ runs (remaining = 0ms, completes)  
4. **10-14ms**: P₁ runs (remaining = 16ms)
5. **14-18ms**: P₁ runs (remaining = 12ms)
6. **18-22ms**: P₁ runs (remaining = 8ms)
7. **22-26ms**: P₁ runs (remaining = 4ms)
8. **26-30ms**: P₁ runs (remaining = 0ms, completes)

**Gantt Chart**:
```
P₁   P₂  P₃  P₁   P₁   P₁   P₁   P₁
0    4   7   10   14   18   22   26   30
```

**Performance Metrics**:
- **Waiting Times**: 
  - P₁ = (0) + (10-4) + (14-10) + (18-14) + (22-18) + (26-22) = 0 + 6 + 4 + 4 + 4 + 4 = 22ms
  - P₂ = (4-0) = 4ms
  - P₃ = (7-0) = 7ms
- **Average Waiting Time**: (22 + 4 + 7)/3 = 11ms

#### Time Quantum Selection ⏰

**Impact of Time Quantum Size**:

**Small Time Quantum (q → 0)**:
- **Advantage**: Better response time, approaches processor sharing
- **Disadvantage**: High overhead due to frequent context switches
- **Extreme Case**: Each process gets 1ms, but context switch takes 1ms → 50% overhead

**Large Time Quantum (q → ∞)**:
- **Advantage**: Low context switching overhead
- **Disadvantage**: Degenerates to FCFS scheduling
- **Poor responsiveness**: Long processes cause delays

**Optimal Time Quantum**:
- **Rule of Thumb**: 80% of CPU bursts should be shorter than time quantum
- **Typical Range**: 10-100 milliseconds
- **Context Switch Time**: Should be < 10% of time quantum
- **System Dependent**: Varies based on system characteristics and workload

#### Time Quantum Examples

**Example with Different Time Quanta**:
**Processes**: P₁ = 6ms, P₂ = 3ms, P₃ = 1ms, P₄ = 7ms

**With q = 1ms**:
```
P₁ P₂ P₃ P₄ P₁ P₂ P₄ P₁ P₂ P₄ P₁ P₄ P₁ P₄ P₁ P₄ P₄
0  1  2  3  4  5  6  7  8  9  10 11 12 13 14 15 16 17
```
- High overhead, many context switches

**With q = 4ms**:  
```
P₁   P₂  P₃ P₄   P₁  P₄
0    4   7  8    12  14   17
```
- Better balance of responsiveness and efficiency

#### Round-Robin Characteristics

**Advantages**:
- **Fair**: Equal CPU time sharing among processes
- **No Starvation**: Every process gets CPU time periodically
- **Good Response Time**: Especially for interactive systems
- **Simple**: Easy to implement and understand
- **Preemptive**: Prevents long processes from monopolizing CPU

**Disadvantages**:
- **Context Switch Overhead**: Frequent preemption causes overhead
- **Poor Average Waiting Time**: Generally higher than SJF
- **Time Quantum Selection**: Difficult to choose optimal value
- **Poor for CPU-bound Processes**: Inefficient for long computations

**Best Suited For**:
- **Time-sharing systems**: Multiple interactive users
- **Interactive systems**: Desktop environments, web servers
- **Real-time systems**: When bounded response time is needed
- **Fair resource allocation**: When equal treatment is important

#### Performance Comparison Summary

**Algorithm Comparison for Same Process Set**:
- **FCFS**: Simple but poor average waiting time, convoy effect
- **SJF**: Optimal average waiting time but potential starvation
- **SRTF**: Better than SJF for mixed arrival times, more overhead
- **Round-Robin**: Fair sharing, good response time, higher average waiting time

**Selection Guidelines**:
- **Batch Systems**: FCFS or SJF
- **Interactive Systems**: Round-Robin
- **Mixed Workload**: Multilevel queue (combining multiple algorithms)
- **Real-time Systems**: Priority-based scheduling

## Key Takeaways 🎯

- **CPU Scheduling** is crucial for multiprogramming systems to maximize CPU utilization and system performance
- **Different metrics** (CPU utilization, throughput, turnaround time, waiting time, response time) serve different system goals
- **FCFS** is simple but suffers from convoy effect and poor performance
- **SJF** provides optimal average waiting time but requires burst time prediction and can cause starvation
- **Round-Robin** ensures fairness and good response time but has context switching overhead
- **Time quantum selection** in Round-Robin significantly impacts system performance
- **No single algorithm** is best for all situations; choice depends on system requirements and workload characteristics
