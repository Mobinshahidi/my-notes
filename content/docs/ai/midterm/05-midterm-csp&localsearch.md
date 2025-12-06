---
title:  csp & local serch, midterm
description: csp & local search, midterm
---


# ⭐ **WEEK 6 — PART 1: Constraint Satisfaction Problems (CSPs)**

CSPs are problems defined by:

### 1️⃣ Variables

### 2️⃣ Domains

### 3️⃣ Constraints

A CSP is a **search problem**, but _instead of searching paths_, you search for **assignments** to variables that satisfy constraints.

---

# 🧩 **1. Variables**

Examples:

- Map coloring:  
    Variables = regions (A, B, C, …)
    
- Sudoku:  
    Variables = 81 cells
    
- N-Queens:  
    Variables = positions of 8 queens
    

---

# 🎨 **2. Domains**

Possible values each variable can take.

Examples:

- Map coloring:
    

$$  
\text{Domain} = { \text{Red}, \text{Green}, \text{Blue} }  
$$

- Sudoku:
    

$$  
{1, 2, 3, \dots, 9}  
$$

- N-Queens:  
    Domain for each queen = column positions
    

---

# 🔗 **3. Constraints**

Constraints may be:

- **Unary** → involve 1 variable
    
- **Binary** → involve 2 variables
    
- **Ternary** → involve 3 variables
    
- **Global** → many variables  
    (e.g., “all different” constraint in Sudoku)
    

Examples:

- Map coloring binary constraint:  
    $$ A \neq B $$
    
- Sudoku row constraint:  
    $$ X_{1,1} \neq X_{1,2} $$
    
- N-Queens attack constraint:  
    $$ |r_i - r_j| \neq |c_i - c_j| $$
    

---

# 🧠 CSP as Search

A CSP solution is an assignment:

$$  
{ X_1 = v_1, X_2 = v_2, \dots, X_n = v_n }  
$$

such that **every constraint** is satisfied.

This is usually solved using:

1. **Backtracking Search**
    
2. **Constraint Propagation**
    
3. **Arc Consistency (AC-3)**
    
4. **Heuristics** (MRV, Degree, Least Constraining Value)
    

All of these appear in CS188 exams.

---

# ⭐ **Backtracking Search**

Basic depth-first search over variable assignments.

### Steps:

1. Pick an unassigned variable
    
2. Choose a value from its domain
    
3. Check consistency with previous assignments
    
4. Continue; if failure → backtrack
    

Backtracking alone is slow → we add heuristics.

---

# ⭐ **Heuristics for CSP**

## 🔥 1. MRV (Minimum Remaining Values)

Choose the variable with the **fewest legal values left**.

Helps avoid early failure.

---

## 🔥 2. Degree Heuristic

Choose the variable that has the **most constraints** on remaining unassigned variables.

This reduces branching.

---

## 🔥 3. LCV (Least Constraining Value)

Pick the value that **rules out the fewest values in neighbors**.

Helps keep options open for future assignments.

---

# ⭐ Constraint Propagation

We eliminate impossible values _before_ search explores them.

Forms:

- **Forward checking**
    
- **Arc consistency (AC-3 algorithm)**
    

---

# ⭐ Arc Consistency (AC-3)

A variable pair ( (X, Y) ) is **arc-consistent** if:

For every value in the domain of (X), there is **some** compatible value in (Y).

AC-3 repeatedly enforces this.

### Arc-consistency condition:

$$  
\forall x \in D(X), ; \exists y \in D(Y) : (x,y) \text{ satisfies constraint}  
$$

If not → remove that x from D(X).

This is exactly the kind of pruning tested in exams.

---

# ⭐ WEEK 6 — PART 2: Local Search

Unlike backtracking (which searches assignments), local search:

- Works on **complete assignments**
    
- Iteratively improves them
    
- Used when state space is huge
    
- Often NOT optimal but very fast
    

Techniques:

1. **Hill Climbing**
    
2. **Simulated Annealing**
    
3. **Genetic Algorithms**
    
4. **Beam Search**
    

These are exam topics in your list.

---

# 🔥 1. Hill Climbing

Start with a complete assignment.  
At each step:

- Look at neighbors
    
- Move to one with better (lower cost)
    

Problem: can get stuck in:

- **local optima**
    
- **plateaus**
    
- **ridges**
    

---

# 🔥 2. Simulated Annealing

Like hill climbing but with randomness.

Accepts _worse_ moves with probability:

$$  
P = e^{-\Delta E / T}  
$$

Where:

- ( \Delta E ) = how much worse the move is
    
- ( T ) = temperature (slowly decreases)
    

At high T → very random  
At low T → greedy like hill climbing

Helps escape local optima.

---

# 🔥 3. Genetic Algorithms (MIT Ranking Trick Included)

Mimics biological evolution.

Population of candidate solutions.  
Each generation:

1. **Selection** — pick best individuals
    
2. **Crossover** — combine parents
    
3. **Mutation** — random noise
    

MIT’s ranking trick:

- Instead of selecting based on score
    
- Convert scores to **ranks**
    
- Selection probability ∝ 1 / rank
    

This stabilizes learning and prevents domination by outliers.

---

# 🔥 4. Beam Search

Similar to BFS but only keep the **k best nodes** at each layer.

Not complete → not optimal  
But very fast in large search spaces.

---

# 🎯 WEEK 6 SUMMARY (Exam-Ready)

### CSP:

- Variables, domains, constraints
    
- Backtracking
    
- MRV, Degree, LCV
    
- Forward checking
    
- Arc consistency (AC-3)
    

### Local Search:

- Hill climbing (limitations)
    
- Simulated annealing
    
- Genetic algorithms (ranking trick)
    
- Beam search
    

---
# ⭐ **بخش ۱ — مسائل ارضای محدودیت (Constraint Satisfaction Problems — CSP)**

در یک CSP، هدف این است که به **تمام متغیرها** مقدار بدهیم به‌طوری‌که **تمام محدودیت‌ها** ارضا شوند.

یک CSP شامل:

### 1️⃣ متغیرها (Variables)

### 2️⃣ دامنه‌ها (Domains)

### 3️⃣ محدودیت‌ها (Constraints)

CSP خودش یک مسئلهٔ جستجو است، اما به‌جای جستجوی مسیر، دنبال **یک انتساب معتبر** برای همهٔ متغیرها هستیم.

---

# 🧩 **۱. متغیرها**

نمونه‌ها:

- رنگ‌آمیزی نقشه:  
    متغیرها = نواحی (A, B, C, …)
    
- سودوکو:  
    ۸۱ خانه
    
- مسئلهٔ ۸ وزیر:  
    متغیرها = موقعیت هر وزیر
    

---

# 🎨 **۲. دامنه‌ها**

دامنهٔ هر متغیر مجموعهٔ مقادیری است که می‌تواند بگیرد.

مثال:

- رنگ‌آمیزی نقشه:  
    $$  
    { \text{Red}, \text{Green}, \text{Blue} }  
    $$
    
- سودوکو:  
    $$  
    {1, 2, ..., 9}  
    $$
    

---

# 🔗 **۳. محدودیت‌ها (Constraints)**

محدودیت‌ها می‌توانند:

- **یک‌متغیره (Unary)**
    
- **دومتغیره (Binary)**
    
- **سه‌متغیره (Ternary)**
    
- **سراسری (Global)** مثل "همه متفاوت باشند" در سودوکو
    

مثال‌ها:

- رنگ‌آمیزی نقشه:  
    $$  
    A \neq B  
    $$
    
- سودوکو:  
    $$  
    X_{1,1} \neq X_{1,2}  
    $$
    
- ۸ وزیر:  
    $$  
    |r_i - r_j| \neq |c_i - c_j|  
    $$
    

---

# ⭐ **CSP به‌عنوان یک مسئلهٔ جستجو**

جواب CSP یک انتساب کامل است:

$$  
{ X_1 = v_1, X_2 = v_2, \dots, X_n = v_n }  
$$

طوری که **تمام محدودیت‌ها برقرار باشند**.

روش‌های حل:

1. جستجوی پس‌گرد (Backtracking Search)
    
2. انتشار محدودیت‌ها (Constraint Propagation)
    
3. سازگاری قوسی (AC-3)
    
4. Heuristicها (MRV, Degree, LCV)
    

---

# ⭐ **جستجوی پس‌گرد (Backtracking Search)**

نسخه‌ای از DFS برای مقداردهی متغیرها.

### مراحل:

1. انتخاب یک متغیر تخصیص‌نیافته
    
2. انتخاب یک مقدار از دامنه
    
3. بررسی سازگاری با انتساب‌های قبلی
    
4. ادامه…
    
5. در صورت تناقض → بازگشت (backtrack)
    

به تنهایی کند است، پس heuristic اضافه می‌کنیم.

---

# ⭐ **Heuristicهای مهم در CSP**

## 🔥 ۱. MRV (Minimum Remaining Values)

متغیری را انتخاب کن که **کم‌ترین تعداد مقدار ممکن** را دارد.

باعث می‌شود سریع‌تر به تناقض‌ها برسیم و کارآمدتر شویم.

---

## 🔥 ۲. Degree Heuristic

متغیری را انتخاب کن که **بیشترین تعداد محدودیت** را روی متغیرهای دیگر اعمال می‌کند.

این کار تعداد شاخه‌های آینده را کم می‌کند.

---

## 🔥 ۳. LCV (Least Constraining Value)

مقداری را انتخاب کن که **کم‌ترین حذف مقدار** را برای متغیرهای دیگر ایجاد می‌کند.

یعنی بیشترین آزادی آینده را حفظ می‌کند.

---

# ⭐ **انتشار محدودیت‌ها (Constraint Propagation)**

هدف: قبل از جستجو، مقادیر نامعتبر را حذف کنیم.

مهم‌ترین روش‌ها:

- **Forward Checking**
    
- **Arc Consistency (AC-3)**
    

---

# ⭐ **سازگاری قوسی (Arc Consistency) — الگوریتم AC-3**

یک قوس (X → Y) **سازگار** است اگر:

برای هر مقدار از دامنهٔ X،  
حداقل یک مقدار در دامنهٔ Y باشد که محدودیت بین آن‌ها را ارضا کند.

### شرط سازگاری:

$$  
\forall x \in D(X),; \exists y \in D(Y); :; (x,y)\ \text{satisfies constraints}  
$$

اگر چنین y وجود نداشته باشد → مقدار x از دامنهٔ X حذف می‌شود.

الگوریتم AC-3 این حذف را به‌صورت تکراری انجام می‌دهد.

---

# ⭐ **بخش ۲ — جستجوی محلی (Local Search)**

برخلاف CSP کلاسیک، جستجوی محلی معمولاً با **یک انتساب کامل** شروع می‌کند و آن را به‌تدریج بهبود می‌دهد.

ویژگی‌ها:

- برای فضاهای حالت بسیار بزرگ
    
- سریع
    
- معمولاً تضمین بهینه بودن ندارد
    
- برای مسائل مانند ۸ وزیر بسیار مناسب است
    

الگوریتم‌ها:

1. Hill Climbing
    
2. Simulated Annealing
    
3. Genetic Algorithms
    
4. Beam Search
    

---

# 🔥 **۱. Hill Climbing**

در هر مرحله:

- به همسایه‌ها نگاه می‌کنیم
    
- به سمت بهترین همسایه حرکت می‌کنیم
    

مشکلات:

- گیر کردن در **بهینه محلی**
    
- سکوها (plateaus)
    
- لبه‌های باریک (ridges)
    

---

# 🔥 **۲. Simulated Annealing**

مانند Hill Climbing اما:

گاهی **حرکات بدتر** را با احتمال:

$$  
P = e^{-\Delta E / T}  
$$

می‌پذیرد.

اینجا:

- ( \Delta E ): مقدار بدتر شدن
    
- ( T ): دما (که کم‌کم کاهش می‌یابد)
    

**T زیاد → رفتار تصادفی**  
**T کم → رفتاری شبیه hill climbing**

به فرار از بهینه‌های محلی کمک می‌کند.

---

# 🔥 **۳. الگوریتم‌های ژنتیک (Genetic Algorithms)**

(+ ترفند رتبه‌بندی MIT)

مراحل:

1. **انتخاب (Selection)** — انتخاب بهترین افراد
    
2. **ترکیب (Crossover)** — ترکیب ژن‌های والدین
    
3. **جهش (Mutation)** — ایجاد تغییر تصادفی
    

### ترفند MIT:

به‌جای انتخاب بر اساس امتیاز خام:

- امتیازها را تبدیل به **رتبه (Rank)** کن
    
- احتمال انتخاب ∝ 1 / rank
    

این باعث پایداری بیشتر و جلوگیری از تسلط یک فرد تصادفی می‌شود.

---

# 🔥 **۴. Beam Search**

نسخه‌ای از BFS اما فقط **k تا بهترین گره** را نگه می‌دارد.

ویژگی‌ها:

- کامل نیست
    
- بهینه نیست
    
- ولی بسیار سریع است
    

---

# 🎯 **خلاصهٔ هفتهٔ ۶ (مخصوص امتحان)**

### CSP:

- متغیرها، دامنه‌ها، محدودیت‌ها
    
- Backtracking
    
- MRV، Degree، LCV
    
- Forward Checking
    
- Arc Consistency (AC-3)
    

### Local Search:

- Hill Climbing
    
- Simulated Annealing
    
- Genetic Algorithms + Ranking Trick
    
- Beam Search
    

---
