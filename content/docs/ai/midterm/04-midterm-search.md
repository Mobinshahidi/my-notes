---
title:  search, midterm
description: search, midterm
---


# 🚀 WEEK 4 — SEARCH ALGORITHMS

Search algorithms help an agent navigate a **state space** to find a path from an initial state to a goal state.  
This is one of the core topics for exams.

---

# ⭐ PART 1 — Search Problem Formulation

A search problem is defined by:

### 1️⃣ State Space
All possible configurations the agent can be in.

### 2️⃣ Initial State
Starting point.

### 3️⃣ Goal Test
Determines whether a state satisfies the objective.

### 4️⃣ Successor Function
Defines available actions and resulting states.

### 5️⃣ Path Cost Function
Cost of a sequence of actions.  
If costs are all 1 → we call it **unit cost**.

---

# ⭐ PART 2 — Uninformed Search Algorithms (Blind Search)

These do **not** use heuristics.

Algorithms:

1. **BFS — Breadth-First Search**  
2. **DFS — Depth-First Search**  
3. **UCS — Uniform Cost Search**  
4. **IDDFS — Iterative Deepening DFS**

---

# 🔵 1. Breadth-First Search (BFS)

Expands nodes in increasing depth.

Uses a **FIFO queue**.

### Algorithm:
1. Put start state into queue.  
2. Pop from queue → expand it.  
3. Add all **unvisited** successors to the queue.  
4. Stop when reaching a goal.

### Properties:

- **Complete:**  
  ✔ Yes (if branching factor finite)

- **Optimal:**  
  ✔ Yes, **only if** all step costs = 1

- **Time Complexity:**  
  $$
  O(b^d)
  $$

- **Space Complexity:**  
  $$
  O(b^d)
  $$

Where:

- \( b \) = branching factor  
- \( d \) = depth of optimal solution  

### When to use:
- When costs = 1  
- When a shallow solution is likely  

---

# 🔵 2. Depth-First Search (DFS)

Expands the deepest node first.

Uses a **stack (LIFO)**.

### Properties:

- **Complete:**  
  ❌ No (fails on infinite trees)

- **Optimal:**  
  ❌ No

- **Time:**  
  $$
  O(b^m)
  $$
  where \(m\) = maximum depth

- **Space:**  
  $$
  O(bm)
  $$

- Very memory efficient.

### When to use:
- Low memory
- Solution is deep
- Tree depth known (rare)

---

# 🔵 3. Uniform Cost Search (UCS)

Generalization of BFS for **varying step costs**.  
Always expands the node with smallest cost-so-far \( g(n) \).

Uses a **priority queue** ordered by \( g(n) \).

### Algorithm:

The priority queue key is:

$$
\text{priority}(n) = g(n)
$$

Expand smallest \(g\).  
When popping the goal → guaranteed optimal.

### Properties:

- **Complete:** ✔  
- **Optimal:** ✔ (if all costs > 0)  
- **Time:**  
  $$
  O(b^{1 + \lfloor C^*/\epsilon \rfloor})
  $$
  where \(C^*\) = optimal cost, \(\epsilon\) = minimum action cost

- **Space:** Same as time.

### When to use:
- Non-uniform step costs  
- Must find cheapest route  

---

# 🔵 4. Iterative Deepening DFS (IDDFS)

Combines:

- BFS’s completeness + optimality  
- DFS’s memory efficiency  

### How it works:
For depth limit \(L = 0, 1, 2, ...\):

1. Run DFS with depth limit \(L\).  
2. If found goal → stop.  

### Properties:

- **Complete:** ✔  
- **Optimal:** ✔ (for unit costs)  
- **Time:**  
  $$
  O(b^d)
  $$

- **Space:**  
  $$
  O(bd)
  $$

### When to use:
- Tree is very deep  
- Memory is limited  
- Costs are uniform  

---

# ⭐ PART 3 — Informed Search (A\*)

A\* uses a heuristic to guide search.

It evaluates each node with:

$$
f(n) = g(n) + h(n)
$$

Where:

- \( g(n) \): cost so far  
- \( h(n) \): heuristic estimate to goal  

A\* expands lowest \( f(n) \) first.

Uses a **priority queue**.

---

# ⭐ PART 4 — Heuristics

A heuristic \(h(n)\) estimates the cost from \(n\) to the goal.

### Examples:

- **Manhattan distance** for grid world:

$$
h(n) = |x - x_g| + |y - y_g|
$$

- **Misplaced tiles** (8-puzzle)

- **Euclidean distance**

---

## 🔶 Admissibility

A heuristic is **admissible** if:

$$
h(n) \leq h^*(n)
$$

for **every** node \(n\), where \(h^*(n)\) is the true remaining cost.

### Meaning:
It **never overestimates**.

**Admissibility ⇒ A\* is optimal.**

---

## 🔶 Consistency (Monotonicity)

A heuristic is consistent if:

$$
h(n) \leq c(n, n') + h(n')
$$

for every successor \(n'\).

### Meaning:
The heuristic obeys a triangle inequality.

### Important facts:

- Every consistent heuristic is admissible.  
- If a heuristic is consistent, **A\* never needs to reopen nodes**.  
- This makes A\* efficient.

---

# ⭐ PART 5 — A\* Algorithm Details

### Priority queue key:

$$
f(n) = g(n) + h(n)
$$

### A\* pseudocode (conceptual):


Initialize frontier with start state
Set g(start) = 0
While frontier not empty:
n = node with lowest f(n)
If n satisfies goal test:
return solution
For each successor s of n:
compute g(s)
if s not seen or new g(s) is better:
update best path
push/update s in frontier

A\* always expands the node that looks best considering **past cost + heuristic estimate**.

---

# ⭐ PART 6 — Comparison Table (Exam Cheat Sheet)

| Algorithm | Complete | Optimal | Time | Space | Notes |
|----------|----------|---------|-------|--------|-------|
| BFS | ✔ | ✔ (unit cost) | \(O(b^d)\) | \(O(b^d)\) | Explores shallowest nodes |
| DFS | ❌ | ❌ | \(O(b^m)\) | \(O(bm)\) | May get stuck deep |
| UCS | ✔ | ✔ | large | large | Best uninformed for non-uniform costs |
| IDDFS | ✔ | ✔ (unit cost) | \(O(b^d)\) | \(O(bd)\) | Best uninformed overall |
| A\* | ✔ | ✔ (if \(h\) admissible) | varies | varies | Best informed search |

---

# ⭐ PART 7 — Practice Concepts You MUST Know for Exams

1. **Identify state space, successors, goal test, cost function**  
2. **Trace BFS, DFS, UCS, A\***  
3. **Compute \(g(n)\), \(h(n)\), \(f(n)\)**  
4. **Check heuristic admissibility**  
5. **Check heuristic consistency**  
6. **Explain algorithm properties**  

---

# ⭐ PART 8 — Example: A\* Computation (Structure)

Given a node:

- \(g(n) = 5\)  
- \(h(n) = 7\)

Compute:

$$
f(n) = g(n) + h(n) = 12
$$

Priority queue picks smallest f-value.

We will solve full examples later if needed.

---

# 🎯 WEEK 4 SUMMARY (Exam-Ready)

### Concepts:
- Search problem formulation  
- Uninformed search  
- Informed search  
- Heuristic design  
- A\* properties  

### Algorithms to MEMORIZE:
- BFS  
- DFS  
- UCS  
- IDDFS  
- A\*  

### Properties to MEMORIZE:
- completeness  
- optimality  
- time complexity  
- space complexity  

---
# 🚀 هفته ۴ — الگوریتم‌های جستجو (Search Algorithms)

الگوریتم‌های جستجو به یک عامل (agent) کمک می‌کنند تا در یک **فضای حالت (state space)** حرکت کند و از حالت اولیه به حالت هدف برسد.  

این موضوع یکی از مهم‌ترین بخش‌های امتحان میان‌ترم است.

---

# ⭐ بخش ۱ — تعریف مسئلهٔ جستجو (Search Problem Formulation)

یک مسئلهٔ جستجو با این موارد مشخص می‌شود:

### 1️⃣ فضای حالت (State Space)
تمام پیکربندی‌های ممکن که عامل می‌تواند در آن‌ها باشد.

### 2️⃣ حالت اولیه (Initial State)
جایی که عامل شروع می‌کند.

### 3️⃣ آزمون هدف (Goal Test)
چک می‌کند آیا حالت فعلی یک حالت هدف است یا نه.

### 4️⃣ تابع جانشین (Successor Function)
برای هر حالت، اعمال ممکن و حالت‌های ناشی از آن‌ها را تعریف می‌کند.

### 5️⃣ تابع هزینه مسیر (Path Cost Function)
هزینهٔ طی مسیر از آغاز تا یک حالت.  
اگر همهٔ هزینه‌ها برابر ۱ باشند → این مسئله **unit cost** است.

---

# ⭐ بخش ۲ — الگوریتم‌های جستجوی بدون‌اطلاعات (Uninformed / Blind Search)

این الگوریتم‌ها از هیچ heuristic استفاده نمی‌کنند.

الگوریتم‌ها:

1. BFS — جستجوی سطح‌به-سطح  
2. DFS — جستجوی عمق‌اول  
3. UCS — جستجوی کم‌هزینه‌اول  
4. IDDFS — عمق‌اول تدریجی (Iterative Deepening)

---

# 🔵 1. جستجوی سطح‌به-سطح (BFS)

بازه‌ها را به ترتیب **عمق کم‌تر** گسترش می‌دهد.

از **صف (FIFO)** استفاده می‌کند.

### الگوریتم:
1. حالت شروع را وارد صف کن.  
2. از صف خارج کن → گسترش بده.  
3. همهٔ جانشین‌های **بازدیدنشده** را وارد صف کن.  
4. اگر حالت هدف دیده شد → پایان.

### ویژگی‌ها:

- **کامل:**  
  ✔ بله (اگر b محدود باشد)

- **بهینه:**  
  ✔ بله، **فقط وقتی هزینه‌ها برابر ۱ باشند**

- **پیچیدگی زمانی:**  
  $$
  O(b^d)
  $$

- **پیچیدگی فضایی:**  
  $$
  O(b^d)
  $$

که در آن:

- \( b \) = عامل انشعاب (branching factor)  
- \( d \) = عمق کم‌هزینه‌ترین جواب  

### کاربرد:
- وقتی هزینه همهٔ اعمال یکسان است  
- وقتی جواب کم‌عمق وجود دارد  

---

# 🔵 2. جستجوی عمق‌اول (DFS)

عمیق‌ترین گرهٔ توسعه‌نیافته را گسترش می‌دهد.

از **پشته (LIFO)** استفاده می‌کند.

### ویژگی‌ها:

- **کامل:**  
  ❌ خیر (در درخت بی‌نهایت گیر می‌افتد)

- **بهینه:**  
  ❌ خیر

- **پیچیدگی زمانی:**  
  $$
  O(b^m)
  $$
  \( m \) = حداکثر عمق

- **پیچیدگی فضایی:**  
  $$
  O(bm)
  $$

- بسیار کم‌مصرف در حافظه.

### کاربرد:
- وقتی حافظه کم است  
- جواب در عمق زیاد قرار دارد  
- یا عمق درخت معلوم است  

---

# 🔵 3. جستجوی کم‌هزینه‌اول (UCS)

نسخهٔ تعمیم‌یافتهٔ BFS برای هزینه‌های غیریکسان.

گره‌هایی را گسترش می‌دهد که **کم‌ترین هزینهٔ مسیر تا کنون** را دارند:

$$
g(n)
$$

از **صف اولویت‌دار (priority queue)** استفاده می‌کند.

### کلید صف اولویت:

$$
\text{priority}(n) = g(n)
$$

زمانی که گرهٔ هدف از صف خارج می‌شود → جواب **بهینه** است.

### ویژگی‌ها:

- **کامل:** ✔  
- **بهینه:** ✔ (اگر همهٔ هزینه‌ها > 0 باشند)

- **زمان:**  
  $$
  O(b^{1 + \lfloor C^*/\epsilon \rfloor})
  $$
  \(C^*\) = هزینهٔ بهینه  
  \(\epsilon\) = حداقل هزینهٔ یک عمل

- **فضا:** مشابه زمان

### کاربرد:
- هزینهٔ اعمال متفاوت است  
- نیاز به کم‌هزینه‌ترین مسیر داریم  

---

# 🔵 4. عمق‌اول تدریجی (IDDFS)

ترکیب مزایای BFS و DFS:

- کامل مانند BFS  
- کم‌حافظه مانند DFS  

### روش کار:
برای \( L = 0, 1, 2, ... \):

1. DFS را با محدودیت عمق \(L\) اجرا کن  
2. اگر جواب یافت شد → پایان  

### ویژگی‌ها:

- **کامل:** ✔  
- **بهینه:** ✔ (وقتی هزینه واحد باشد)

- **زمان:**  
  $$
  O(b^d)
  $$

- **فضا:**  
  $$
  O(bd)
  $$

### کاربرد:
- درخت بسیار عمیق  
- حافظه محدود  
- هزینه‌ها یکسان  

---

# ⭐ بخش ۳ — جستجوی آگاهانه (Informed Search)

مهم‌ترین الگوریتم: **A\***

A\* از دو مؤلفه استفاده می‌کند:

- هزینه گذشته: \( g(n) \)  
- تخمین هزینهٔ باقیمانده: \( h(n) \)

### تابع ارزیابی:

$$
f(n) = g(n) + h(n)
$$

A\* گره‌هایی را گسترش می‌دهد که **کم‌ترین مقدار f** را دارند.

از **صف اولویت‌دار** استفاده می‌کند.

---

# ⭐ بخش ۴ — Heuristicها

یک heuristic تخمینی از فاصله تا هدف است.

### مثال‌ها:

- فاصلهٔ منهتن:

$$
h(n) = |x - x_g| + |y - y_g|
$$

- تعداد کاشی‌های misplaced (در 8-puzzle)
- فاصلهٔ اقلیدسی

---

## 🔶 قابلیت پذیرش (Admissibility)

یک heuristic **قابل پذیرش** است اگر:

$$
h(n) \leq h^*(n)
$$

برای همهٔ حالت‌ها.

یعنی **هیچ‌وقت بیش‌تخمین نزند**.

### نتیجهٔ مهم:
اگر \(h\) قابل پذیرش باشد → **A\*** بهینه است.

---

## 🔶 سازگاری (Consistency)

یک heuristic **سازگار** است اگر:

$$
h(n) \leq c(n,n') + h(n')
$$

برای همهٔ جانشین‌ها.

### معنی:
یک نابرابری مثلثی را رعایت می‌کند.

### حقایق مهم:

- هر heuristic سازگار → قابل پذیرش هم هست  
- با heuristic سازگار، A\* **هیچ‌گاه گره‌ها را دوباره باز نمی‌کند**  
- اجرای A\* بسیار کارآمدتر می‌شود  

---

# ⭐ بخش ۵ — جزئیات کامل الگوریتم A\*

### کلید صف اولویت:

$$
f(n) = g(n) + h(n)
$$

### شبه‌کد مفهومی:

frontier = {start}  
g(start) = 0

while frontier not empty:  
n = node with lowest f(n)  
if goal(n):  
return solution  
for each successor s of n:  
compute g(s)  
if s is new or g(s) improved:  
record best path to s  
update/insert s in frontier

---

# ⭐ بخش ۶ — جدول مقایسه (Cheat Sheet)

| الگوریتم | کامل؟ | بهینه؟ | زمان | فضا | نکته |
|----------|--------|---------|--------|---------|-------|
| BFS | ✔ | ✔ (هزینه واحد) | \(O(b^d)\) | \(O(b^d)\) | گره‌های کم‌عمق را گسترش می‌دهد |
| DFS | ❌ | ❌ | \(O(b^m)\) | \(O(bm)\) | حافظه کم، اما ممکن است گیر کند |
| UCS | ✔ | ✔ | زیاد | زیاد | بهترین جستجوی بدون‌اطلاعات برای هزینه‌های متفاوت |
| IDDFS | ✔ | ✔ (هزینه واحد) | \(O(b^d)\) | \(O(bd)\) | بهترین جستجوی Blind |
| A\* | ✔ | ✔ (اگر \(h\) قابل پذیرش باشد) | وابسته | وابسته | بهترین الگوریتم آگاهانه |

---

# ⭐ بخش ۷ — مفاهیم مهم برای امتحان

1. تشخیص فضای حالت، تابع جانشین، تست هدف  
2. شبیه‌سازی BFS، DFS، UCS، A\*  
3. محاسبهٔ \(g(n)\)، \(h(n)\)، \(f(n)\)  
4. بررسی admissible بودن heuristic  
5. بررسی consistent بودن heuristic  
6. فهم ویژگی‌ها (کامل، بهینه، زمان، فضا)  

---

# ⭐ بخش ۸ — مثال ساختاری از A\*

اگر:

- \(g(n) = 5\)  
- \(h(n) = 7\)

آنگاه:

$$
f(n) = g(n) + h(n) = 12
$$

کوچک‌ترین \(f\) از صف انتخاب می‌شود.

---

# 🎯 خلاصهٔ هفته ۴ (مخصوص امتحان)

### مفاهیم:
- تعریف مسئلهٔ جستجو  
- جستجوی بدون‌اطلاعات  
- جستجوی آگاهانه  
- heuristic  
- ویژگی‌های A\*  

### الگوریتم‌هایی که باید حفظ باشید:
- BFS  
- DFS  
- UCS  
- IDDFS  
- A\*  

### ویژگی‌هایی که باید بدانید:
- کامل؟  
- بهینه؟  
- پیچیدگی زمان و فضا  

