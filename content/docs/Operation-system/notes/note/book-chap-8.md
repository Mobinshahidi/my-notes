---
title: book, chap 8
description: book, chap 8
---


# Chapter 8: Deadlocks 🔒

## 8.1 System Model 🏗️

### 8.1.1 Resource Types and Instances

A system consists of a finite number of resources to be distributed among competing processes:
- **Resource types**: CPU cycles, memory space, I/O devices, files, semaphores, etc.
- **Resource instances**: Each resource type may have multiple identical instances
- **Example**: A system might have 2 printers (2 instances of printer resource type)

### 8.1.2 Resource Allocation Process

Each process utilizes a resource in the following sequence:
1. **Request**: Process requests the resource (may need to wait if unavailable)
2. **Use**: Process operates on the resource  
3. **Release**: Process releases the resource

### 8.1.3 System Call Interface

The operating system provides system calls for resource management:
- **request()**: Request a resource instance
- **release()**: Release a resource instance
- **open()** and **close()** for files
- **allocate()** and **deallocate()** for memory
- **wait()** and **signal()** for semaphores

### 8.1.4 Resource Allocation Rules

- A process may request as many resources as it needs to perform its designated task
- A process cannot request more resources than are available in the system
- The number of resources requested may not exceed the total number of resources available in the system

## 8.2 Deadlock Characterization 🎯

### 8.2.1 Deadlock Definition

**Deadlock**: A situation where a set of blocked processes each holding a resource and waiting for a resource that can only be released by another process in the set.

### 8.2.2 The Four Necessary Conditions (Coffman Conditions)

A deadlock situation can arise **if and only if** all four of the following conditions hold simultaneously:

#### 1. Mutual Exclusion 🚫
- At least one resource must be held in a non-sharable mode
- Only one process at a time can use the resource
- If another process requests the resource, it must be delayed until the resource is released
- **Example**: A printer cannot be simultaneously shared by several processes

#### 2. Hold and Wait 🤝⏳
- A process must be holding at least one resource and waiting to acquire additional resources held by other processes
- Process holds allocated resources while waiting for others
- **Example**: Process A holds resource R1 and requests R2, which is held by Process B

#### 3. No Preemption 🔒
- Resources cannot be preempted (forcibly removed)
- A resource can be released only voluntarily by the process holding it
- After the process has completed its task
- **Example**: You cannot forcibly take away a file that a process is currently writing to

#### 4. Circular Wait 🔄
- A set {P₀, P₁, ..., Pₙ} of waiting processes must exist such that:
  - P₀ is waiting for a resource held by P₁
  - P₁ is waiting for a resource held by P₂
  - ...
  - Pₙ₋₁ is waiting for a resource held by Pₙ
  - Pₙ is waiting for a resource held by P₀
- **Example**: Process A waits for Process B, Process B waits for Process C, Process C waits for Process A

### 8.2.3 Resource Allocation Graph (RAG)

A directed graph used to describe deadlocks more precisely:

#### Graph Components
- **Vertices (V)**: Set of all processes P = {P₁, P₂, ..., Pₙ} and all resource types R = {R₁, R₂, ..., Rₘ}
- **Edges (E)**: Directed edges between processes and resources

#### Edge Types
- **Request Edge**: Directed edge Pᵢ → Rⱼ indicates process Pᵢ has requested resource type Rⱼ and is currently waiting
- **Assignment Edge**: Directed edge Rⱼ → Pᵢ indicates an instance of resource type Rⱼ has been allocated to process Pᵢ

#### Graph Representation
- **Process**: Represented by a circle
- **Resource Type**: Represented by a rectangle
- **Resource Instance**: Represented by a dot within the resource rectangle

#### Deadlock Detection Using RAG
- **If graph contains no cycles**: No deadlock exists
- **If graph contains cycles**:
  - If only one instance per resource type → deadlock exists
  - If several instances per resource type → deadlock may exist

### 8.2.4 Deadlock vs Starvation

- **Deadlock**: Processes are blocked indefinitely waiting for each other
- **Starvation**: A process waits indefinitely due to resource allocation policies, but system continues to make progress

## 8.3 Methods for Handling Deadlocks 🛠️

There are three principal methods for dealing with the deadlock problem:

### 8.3.1 Deadlock Prevention 🚧
- Ensure that at least one of the four necessary conditions cannot hold
- **Approach**: Design the system to eliminate the possibility of deadlock
- **Advantage**: Deadlock never occurs
- **Disadvantage**: May lead to low device utilization and reduced system throughput

### 8.3.2 Deadlock Avoidance 🎯
- Allow the system to enter an unsafe state but use additional information to avoid deadlock
- **Approach**: Require additional information about resource requests in advance
- **Key Concept**: Safe state vs unsafe state
- **Advantage**: More flexible than prevention
- **Disadvantage**: Requires advance knowledge of resource requirements

### 8.3.3 Deadlock Detection and Recovery 🔍🚑
- Allow deadlocks to occur, then detect and recover from them
- **Approach**: Periodically run a deadlock detection algorithm
- **Advantage**: No restrictions on resource requests
- **Disadvantage**: Overhead of detection algorithm and recovery process

### 8.3.4 Ignore the Problem (Ostrich Algorithm) 🦆
- Pretend that deadlocks never occur in the system
- **Used by**: Most operating systems including UNIX and Windows
- **Reasoning**: Deadlocks occur infrequently, and the cost of prevention/avoidance/detection may be higher than occasional system restart
- **Trade-off**: Accept occasional deadlock for better performance

## 8.4 Deadlock Prevention 🛡️

Deadlock prevention ensures that at least one of the four necessary conditions cannot hold.

### 8.4.1 Eliminating Mutual Exclusion 🚫❌

**Approach**: Make resources sharable when possible

**Method**:
- Some resources are inherently non-sharable (e.g., mutex locks, printers)
- Read-only files can be shared
- Make as many resources as possible sharable

**Limitations**:
- Not applicable to all resources
- Some resources cannot be shared by nature
- May not be practical for many resource types

**Example**: Multiple processes can read the same file simultaneously, but only one can write at a time

### 8.4.2 Eliminating Hold and Wait 🤝❌

**Approach**: Guarantee that when a process requests a resource, it does not hold any other resources

#### Method 1: Request All Resources at Once
- Process must request and be allocated all resources before execution begins
- **Advantage**: Simple to implement
- **Disadvantages**:
  - Low resource utilization (resources allocated but unused for long periods)
  - Starvation possible (process may wait indefinitely for all resources)
  - Difficult to know all required resources in advance

#### Method 2: Release All Resources Before New Request
- Process releases all currently held resources before requesting new ones
- Must re-request all resources it needs (including previously held ones)
- **Advantage**: No hold and wait condition
- **Disadvantages**:
  - Work may be lost when resources are released
  - Increased overhead due to repeated requests/releases

**Example**: A process copying data from tape to disk to printer must request tape, disk, and printer all at once

### 8.4.3 Eliminating No Preemption 🔒❌

**Approach**: Allow preemption of resources when necessary

#### Method 1: Resource Preemption on Request Failure
- If a process holding resources requests another resource that cannot be immediately allocated:
  1. Preempt all resources currently held by the requesting process
  2. Add these resources to the list of resources for which the process is waiting
  3. Process restarts only when it can regain old resources plus new ones

#### Method 2: Preemption Based on Waiting Processes
- If a process requests resources held by waiting processes:
  1. Preempt desired resources from waiting processes
  2. Allocate preempted resources to requesting process
  3. Waiting process restarts when all required resources are available

**Limitations**:
- Generally applied to resources whose state can be easily saved and restored (CPU registers, memory)
- Cannot be applied to resources like mutex locks and semaphores
- May cause indefinite postponement (starvation)

**Example**: CPU can be preempted (context switch), but a printer in the middle of printing cannot be preempted

### 8.4.4 Eliminating Circular Wait 🔄❌

**Approach**: Impose total ordering on all resource types

#### Method: Resource Ordering Protocol
1. **Define ordering**: Assign a unique integer number to each resource type R₁, R₂, ..., Rₘ
2. **Ordering rule**: Each process requests resources in increasing order of enumeration number
3. **Release rule**: Resources can be released in any order

#### Formal Protocol
- Let F: R → N be a function defining the ordering (where N is natural numbers)
- Process can request resources Rᵢ only if F(Rᵢ) > F(Rⱼ) for all resources Rⱼ currently held

#### Alternative Protocol
- A process can request resource Rᵢ, then resource Rⱼ (where F(Rⱼ) > F(Rᵢ)) only after releasing all resources Rₖ where F(Rₖ) ≥ F(Rⱼ)

**Proof of Correctness**:
- Assume circular wait exists: P₀ → R₁ → P₁ → R₂ → ... → Rₙ → P₀
- Since Pᵢ₊₁ holds Rᵢ₊₁ and requests Rᵢ₊₂, we have F(Rᵢ₊₁) < F(Rᵢ₊₂)
- Following the chain: F(R₁) < F(R₂) < ... < F(Rₙ) < F(R₁)
- This implies F(R₁) < F(R₁), which is impossible
- Therefore, circular wait cannot exist

**Example Ordering**:
- R₁ = card reader (F(R₁) = 1)
- R₂ = disk drive (F(R₂) = 5)  
- R₃ = printer (F(R₃) = 12)

**Disadvantages**:
- May not always be possible to find ordering that satisfies all applications
- May result in resource underutilization
- Applications must be written to comply with ordering

## 8.5 Deadlock Avoidance 🎯

Deadlock avoidance requires additional information about resource allocation requests.

### 8.5.1 Safe State Concept 💚

**Safe State**: A state where there exists a sequence of all processes in the system such that for each process Pᵢ in the sequence, the resources that Pᵢ can still request can be satisfied by currently available resources plus resources held by all processes Pⱼ where j < i.

#### Safe Sequence
A sequence <P₁, P₂, ..., Pₙ> is safe for the current allocation state if:
- For each Pᵢ, the resource requests that Pᵢ can still make can be satisfied by:
  - Currently available resources +
  - Resources held by all processes Pⱼ where j < i

#### Safe State Properties
- **If system is in safe state**: No deadlock exists
- **If system is in unsafe state**: Possibility of deadlock exists
- **Avoidance strategy**: Ensure system never enters unsafe state

#### Safe State Algorithm Execution
1. Initially, only P₁ can complete (resources available satisfy its needs)
2. After P₁ completes, its resources are added to available resources
3. Now P₂ can complete with available + P₁'s released resources
4. Process continues until all processes complete successfully

**Key Insight**: Safe state ≠ Deadlock, Unsafe state ≠ Deadlock (but possible)

### 8.5.2 Resource-Allocation-Graph Algorithm 📊

Used when each resource type has exactly one instance.

#### Graph Modification
- Add **claim edges** to the basic resource allocation graph
- **Claim edge** Pᵢ → Rⱼ: Process Pᵢ may request resource Rⱼ at some time in the future
- **Representation**: Claim edges shown as dashed lines
- **Conversion**: Claim edge converts to request edge when process actually requests the resource

#### Safety Check Algorithm
Before granting a request edge Pᵢ → Rⱼ:
1. Convert request edge to assignment edge Rⱼ → Pᵢ
2. Check if resulting graph has cycles
3. **If cycle exists**: Request cannot be granted (would lead to unsafe state)
4. **If no cycle**: Request can be safely granted

#### Graph States
- **Request edge**: Process has requested resource and is waiting
- **Assignment edge**: Resource has been allocated to process  
- **Claim edge**: Process may request resource in future

**Example Cycle Detection**: If granting a request creates a cycle in the graph, the request must be denied to maintain safety.

### 8.5.3 Banker's Algorithm 🏛️

Used when each resource type can have multiple instances. Named after the way banks manage loans to ensure they can satisfy all customers.

#### Data Structures (for n processes and m resource types)

**Available[m]**: 
- Number of available instances of each resource type
- Available[j] = k means k instances of resource type Rⱼ are available

**Max[n][m]**: 
- Maximum demand matrix
- Max[i][j] = k means process Pᵢ may request at most k instances of resource type Rⱼ

**Allocation[n][m]**: 
- Current allocation matrix
- Allocation[i][j] = k means process Pᵢ is currently allocated k instances of resource type Rⱼ

**Need[n][m]**: 
- Remaining need matrix
- Need[i][j] = k means process Pᵢ may need k more instances of resource type Rⱼ
- **Formula**: Need[i][j] = Max[i][j] - Allocation[i][j]

#### Safety Algorithm

**Purpose**: Determine if the current state is safe

**Algorithm Steps**:
1. **Initialize**:
   - Work = Available (working copy of available resources)
   - Finish[i] = false for all i (tracks completed processes)

2. **Find Process**: Find index i such that:
   - Finish[i] == false AND
   - Need[i] ≤ Work (process can complete with available resources)

3. **Complete Process**:
   - Work = Work + Allocation[i] (add released resources)
   - Finish[i] = true (mark as completed)

4. **Check Completion**:
   - If Finish[i] == true for all i: System is in safe state
   - Otherwise: System is in unsafe state

**Time Complexity**: O(m × n²) where m = resource types, n = processes

#### Resource-Request Algorithm

**Purpose**: Determine if a request can be safely granted

**Request Processing for Process Pᵢ**:
Let Request[i] be the request vector for process Pᵢ

**Step 1 - Validity Check**:
- If Request[i] ≤ Need[i]: Continue to step 2
- Otherwise: Error (process exceeded maximum claim)

**Step 2 - Resource Availability Check**:
- If Request[i] ≤ Available: Continue to step 3  
- Otherwise: Process must wait (insufficient resources)

**Step 3 - Tentative Allocation**:
```
Available = Available - Request[i]
Allocation[i] = Allocation[i] + Request[i]  
Need[i] = Need[i] - Request[i]
```

**Step 4 - Safety Check**:
- Run Safety Algorithm on new state
- **If safe**: Allocation is permanent
- **If unsafe**: Restore original state and make process wait

#### Banker's Algorithm Example

**System State**:
- 5 processes: P₀, P₁, P₂, P₃, P₄
- 3 resource types: A, B, C with instances (10, 5, 7)

**Current State**:
```
Available = [3, 3, 2]

         Allocation    Max       Need
         A  B  C      A  B  C    A  B  C
    P₀   0  1  0      7  5  3    7  4  3
    P₁   2  0  0      3  2  2    1  2  2  
    P₂   3  0  2      9  0  2    6  0  0
    P₃   2  1  1      2  2  2    0  1  1
    P₄   0  0  2      4  3  3    4  3  1
```

**Safety Check**:
1. Work = [3,3,2], all Finish[i] = false
2. Only P₁ and P₃ have Need ≤ Work
3. Execute P₁: Work = [5,3,2], Finish[1] = true
4. Execute P₃: Work = [7,4,3], Finish[3] = true  
5. Execute P₄: Work = [7,4,5], Finish[4] = true
6. Execute P₂: Work = [10,4,7], Finish[2] = true
7. Execute P₀: Work = [10,5,7], Finish[0] = true

**Safe sequence**: <P₁, P₃, P₄, P₂, P₀>

### 8.5.4 Limitations of Deadlock Avoidance

**Practical Limitations**:
- Requires advance knowledge of maximum resource needs
- Number of processes must be fixed
- Resources cannot be added/removed dynamically
- Processes cannot exit while holding resources

**Performance Issues**:
- Conservative approach leads to resource underutilization
- Safety algorithm overhead on every resource request
- May reject requests that wouldn't actually cause deadlock

**Real-world Applicability**:
- Rarely used in general-purpose operating systems
- More suitable for specialized systems with predictable resource usage
- Banking and embedded systems where resource patterns are well-defined

## Key Takeaways 🎯

- **Deadlock occurs** when four conditions hold simultaneously: mutual exclusion, hold and wait, no preemption, and circular wait
- **Prevention** eliminates one of the four necessary conditions but may reduce system efficiency
- **Avoidance** maintains the system in a safe state using advance information about resource requirements
- **Resource Allocation Graphs** help visualize deadlock situations and detect potential deadlocks
- **Banker's Algorithm** provides a systematic approach to deadlock avoidance in multi-instance resource systems
- **Trade-offs exist** between deadlock handling approaches: prevention/avoidance provide safety but reduce performance, while detection/recovery allows better resource utilization but requires recovery mechanisms
