# Week 1 – Part 2: Linear Optimization (LP)

Linear Optimization (Linear Programming, LP) is about choosing the best values for variables when both the **objective** and **constraints** are linear.  
LP forms the mathematical foundation for many AI problems.

---

# 1. What Is a Linear Program?

A Linear Program (LP) consists of:

---

## 1.1 Objective Function (Linear)

Examples:

Minimization:
$$
\min(3x + 4y)
$$

Maximization:
$$
\max(5x - 2y)
$$

The key requirement: **no powers, no products of variables.**

---

## 1.2 Linear Constraints

Each constraint must be a linear inequality or equality.

Example:

$$
\begin{aligned}
2x + y &\le 10 \\
-3x + 4y &\ge 5 \\
x, y &\ge 0
\end{aligned}
$$

Invalid constraints include:

- quadratic:  $$x^2 + y \le 3$$  
- product:  $$xy \ge 7$$  
- absolute:  $$|x| \le 4$$  
- trigonometric:  $$\sin(x) + y \le 2$$  

These are **not LP**.

---

# 2. Recognizing Whether a Problem *Is* an LP

A problem *is* an LP if:

- The objective is linear  
- Every constraint is linear  
- Variables only appear with power 1  
- No non-linear operations  

**Checklist:**  
- ❌ No exponents  
- ❌ No variable × variable  
- ❌ No `max(x,y)` inside constraints  
- ❌ No logic conditions (“if x then …”)  

---

# 3. LP in Standard Form

General LP (minimization version):

### Objective:
$$
\min(c_1x_1 + c_2x_2 + \dots + c_nx_n)
$$

### Subject to:
$$
\begin{aligned}
a_{11}x_1 + a_{12}x_2 + \dots + a_{1n}x_n &\ge b_1 \\
\vdots \\
x_1, x_2, \dots, x_n &\ge 0
\end{aligned}
$$

---

## 3.1 Converting Constraints

If you have:

$$
ax + by \le c
$$

Multiply by \( -1 \):

$$
-ax - by \ge -c
$$

---

## 3.2 Handling Equalities

Equality:

$$
ax + by = c
$$

is equivalent to:

$$
ax + by \ge c
$$

and

$$
ax + by \le c
$$

(Then convert the ( $\le$) to ( $\ge$ ) if needed.)

---

# 4. Feasible Region (Geometric Interpretation)

Each constraint defines a **half-space**.  
The intersection of half-spaces creates the **feasible region**, which is always **convex**.

Mathematically:

If points \( x \) and \( y \) satisfy all constraints, then:

$$
z = \lambda x + (1 - \lambda) y
$$

also satisfies constraints for any:

$$
0 \le \lambda \le 1
$$

This convexity is why LP is easy to solve compared to non-linear problems.

---

# 5. The Corner Point Method (Graphical LP Solving)

Used for LPs with 2 variables.

### Steps:

1. Convert each constraint to an equality and draw the lines  
2. Shade or determine the feasible side  
3. Find all corner points (intersections)  
4. Keep only feasible intersections  
5. Evaluate the objective at each feasible corner  
6. Choose the best (min or max)

---

## 5.1 Important Theorem

**The optimum of a linear program (if it exists) occurs at a corner of the feasible region.**

This is why evaluating only corners is sufficient.

---

# 6. Types of LP Solutions

---

## 6.1 Bounded Solution

The feasible region is closed and limited.  
An optimal point exists at a vertex.

---

## 6.2 Unbounded LP

The feasible region extends infinitely in the direction where the objective improves.

Example:

Objective:
$$
\min x
$$

Constraints:
$$
x \ge 0, \quad y \ge 0
$$

No lower bound on \(x\) → unbounded.

---

## 6.3 Infeasible LP

Constraints conflict — no point satisfies all.

Example:
$$
x \ge 5,\quad x \le 2
$$

---

## 6.4 Infinite Optimal Solutions

Occurs when the objective function is **parallel** to a boundary edge.

Example:

Objective:
$$
\min(x + y)
$$

Constraint boundary:
$$
x + y = 10
$$

Every point on that edge is optimal.

---

# 7. Example LP (Classic Diet Problem)

Let:

$$
x = \text{apples},\quad y = \text{bananas}
$$

Objective:
$$
\min(2x + y)
$$

Constraints:
$$
\begin{aligned}
4x + 2y &\ge 20 \\
x + 2y &\ge 15 \\
x, y &\ge 0
\end{aligned}
$$

This is a valid LP.

---

# 8. Practice LP Example

Variables:

$$
x = \text{small boxes},\quad y = \text{large boxes}
$$

Objective:
$$
\min(2x + 5y)
$$

Constraints:
$$
\begin{aligned}
x + y &\ge 10 \\
2x + 5y &\le 40 \\
x, y &\ge 0
\end{aligned}
$$

---

# 9. LP Cheat Sheet (Exam-Ready)

### An LP must have:
- Linear objective  
- Linear constraints  
- Non-negative variables (in standard form)

### Method for solving by hand:
- Plot constraints  
- Find intersections  
- Keep feasible corners  
- Evaluate objective  
- Select optimum  

### Three special cases:
- **Unbounded**  
- **Infeasible**  
- **Infinite optimal solutions**  

---

# 🎯 **Part 1 — LP Formulation (The Real Skill Tested in Exams)**

The *most important* Week 2 skill is:

> **Reading a word problem → turning it into variables + objective + constraints**

This is tested heavily in assignments & interviews.

We follow a systematic 4-step process.

---

# 1️⃣ Step 1: Define Decision Variables

Example:

Let a factory produce chairs and tables:

* ( x = \text{number of chairs} )
* ( y = \text{number of tables} )

Variables must always be:

$$
x, y \ge 0
$$

---

# 2️⃣ Step 2: Write the Objective Function

Example: maximize profit

* Profit per chair = 30
* Profit per table = 50

Objective:

$$
\max(30x + 50y)
$$

---

# 3️⃣ Step 3: Write the Constraints

If labor hours limit is:

$$
2x + 4y \le 100
$$

And wood usage is:

$$
3x + 2y \le 90
$$

These become linear constraints.

---

# 4️⃣ Step 4: Non-negativity Constraints

Always include:

$$
x, y \ge 0
$$

---

# ✔️ FULL Week 2 Example (classic LP problem)

A farmer wants to buy cows and goats.

* Cow requires:

  * 3 hours attention
  * 5 units food
  * profit = 40
* Goat requires:

  * 1 hour attention
  * 2 units food
  * profit = 15

Limits:

* Total attention = 24
* Total food = 30

### Variables:

$$
c = \text{number of cows},\quad g = \text{number of goats}
$$

### Objective:

$$
\max(40c + 15g)
$$


Great — you now fully understand Week 1 (State Spaces + Linear Optimization).
Time to move forward to ￼￼Week 2￼￼, exactly as your syllabus specifies.

### Constraints:

$$
\begin{aligned}
3c + g &\le 24 \
5c + 2g &\le 30 \
c, g &\ge 0
\end{aligned}
$$

This is a fully correct LP.

If asked to solve it, we use Corner Point Method.

---

# 🔥 **EXAM SKILL: TURN ANY TEXT INTO AN LP**

Your midterm might give a scenario like:

> A company must ship packages using trucks and vans, each with different capacities and costs…

Or:

> A diet must contain at least X protein and Y carbs but minimize cost…

Or:

> A robot must allocate time among tasks under resource constraints…

You always respond with:

* Variables
* Objective
* Constraints
* Non-negativity

I can prepare a full set of exam-style LP practice later if you want.

---

# 🧩 **Part 2 — Integer Linear Programming (ILP)**

This is the NEW concept in Week 2.

ILP = LP with integer requirements:

Example:
$$
x, y \in \mathbb{Z}_{\ge 0}
$$

or:

$$
x \in {0, 1}
$$

### ❗ BIG DIFFERENCE:

* **LP is easy** → solvable in polynomial time
* **ILP is hard (NP-complete)**

Why?
Because integers break convexity.

Example LP feasible region = convex polygon.
ILP feasible region = isolated points (hard to search).

---

# ⭐ Types of Integer Optimization

### 1. Pure ILP

All variables integer
$$
x, y \in \mathbb{Z}
$$

### 2. Mixed Integer LP (MILP)

Some variables integer
$$
x \in \mathbb{Z},; y \in \mathbb{R}
$$

### 3. Binary ILP (most important)

Variables are 0 or 1
$$
x \in {0,1}
$$

Used heavily in:

* scheduling
* choosing projects
* selecting actions
* decision making

---

# 🎯 Example of Binary ILP

A robot chooses tasks A or B:

* Task A uses 3 energy, gives 5 reward
* Task B uses 4 energy, gives 6 reward
* Max energy = 5

Variables:

$$
x_A, x_B \in {0, 1}
$$

Objective:
$$
\max(5x_A + 6x_B)
$$

Constraint:
$$
3x_A + 4x_B \le 5
$$

This forces the robot to choose at most one task.

---

# 🧠 Key contrasts (LP vs ILP)

| Property             | LP             | ILP                |
| -------------------- | -------------- | ------------------ |
| Variables            | real-valued    | integer / binary   |
| Feasible region      | convex polygon | discrete points    |
| Solution method      | corner points  | NP-hard search     |
| Solvable fast?       | yes            | often no           |
| Produces fractional? | sometimes      | never (restricted) |

---

# 📝 **Part 3 — Solving ILP by Relaxation (Very Common)**

Often you:

1. Remove integer restriction → solve LP
2. Round or analyze
3. Check feasibility

If the relaxed LP gives integer solutions → ILP solved
If not → more advanced techniques required (Branch & Bound)

---

# 🔍 Mini Exercise (your turn)

A school buys buses:

* Small bus seats 20 students
* Large bus seats 50 students
* Must carry 180 students
* Minimize number of buses
* Cannot buy fractional buses → integer constraint

Variables:

$$
s = \text{number of small buses} \
l = \text{number of large buses}
$$

Objective?
Min(xs+xl) 
Constraints? Xs,xl>=0 & 20xs+50xl=180
Integer requirements?

If you want, I’ll check your answer.

---

# 🎉 Week 2 Summary (Cheat Sheet)

**LP Formulation**

* Define variables
* Write objective
* Write constraints
* Add non-negativity

**Corner Point Method**

* Evaluate objective at feasible corners

**Solution Types**

* Unique
* None
* Infinite
* Unbounded

**Integer Programming**

* Add integer requirements
* Harder than LP
* Can be relaxed to LP

----
# هفته ۱ – بخش ۲: بهینه‌سازی خطی (Linear Optimization / LP)

بهینه‌سازی خطی (Linear Programming یا LP) مسئله‌ای است که در آن باید بهترین مقدار ممکن برای متغیرها را پیدا کنیم، وقتی که **تابع هدف** و **تمام قیود** همگی **خطی** هستند.

LP یکی از پایه‌های مهم در درس هوش مصنوعی است و بعداً در مباحثی مثل نظریه بازی‌ها، مسائل تصمیم‌گیری، و تحلیل مسائل محدودیت‌دار استفاده می‌شود.

---

# ۱. برنامه‌ریزی خطی چیست؟

یک مسئلهٔ LP شامل موارد زیر است:

---

## ۱.۱ تابع هدف (Objective Function)

نمونه برای کمینه‌سازی:

$$
\min(3x + 4y)
$$

نمونه برای بیشینه‌سازی:

$$
\max(5x - 2y)
$$

تابع هدف **باید خطی باشد**.

---

## ۱.۲ قیود خطی (Linear Constraints)

هر قید باید یک نامساوی یا مساوی خطی باشد.

مثال:

$$
\begin{aligned}
2x + y &\le 10 \\
-3x + 4y &\ge 5 \\
x, y &\ge 0
\end{aligned}
$$

قیود زیر **غیرخطی‌اند و LP محسوب نمی‌شوند**:

- $$x^2 + y \le 3$$  
- $$xy \ge 7$$  
- $$|x| \le 4$$  
- $$\sin(x) + y \le 2$$  

---

# ۲. تشخیص اینکه یک مسئله LP هست یا نه

یک مسئله **LP است اگر و تنها اگر**:

- تابع هدف خطی باشد  
- همهٔ قیود خطی باشند  
- هیچ متغیری توان ۲ یا بیشتر نداشته باشد  
- ضرب متغیرها در هم نباشد  

چک‌لیست سریع:

- ❌ توان‌دار نباشد  
- ❌ ضرب متغیرها نباشد  
- ❌ توابعی مثل sin، max، abs نباشند  

---

# ۳. فرم استاندارد LP

### تابع هدف:

$$
\min(c_1x_1 + c_2x_2 + \dots + c_nx_n)
$$

### قیود:

$$
\begin{aligned}
a_{11}x_1 + a_{12}x_2 + \dots + a_{1n}x_n &\ge b_1 \\
\vdots \\
x_1, x_2, \dots, x_n &\ge 0
\end{aligned}
$$

---

## ۳.۱ تبدیل قیود

اگر قید در فرم زیر باشد:

$$
ax + by \le c
$$

می‌توان آن را با ضرب در ‎\(-1\)‎ به فرم استاندارد تبدیل کرد:

$$
-ax - by \ge -c
$$

---

## ۳.۲ تبدیل مساوی‌ها

یک معادلهٔ خطی:

$$
ax + by = c
$$

معادل است با:

$$
ax + by \ge c
$$

و

$$
ax + by \le c
$$

(و سپس هر کدام را در صورت نیاز به فرم استاندارد تبدیل می‌کنیم).

---

# ۴. ناحیهٔ شدنی (Feasible Region)

هر قید یک **نیم‌فضا** ایجاد می‌کند.  
اشتراک این نیم‌فضاها، ناحیهٔ شدنی را تشکیل می‌دهد.

این ناحیه همیشه **کوژ (convex)** است.

خاصیت کوژ بودن:

$$
z = \lambda x + (1 - \lambda)y
$$

برای هر:

$$
0 \le \lambda \le 1
$$

نیز شدنی است.

---

# ۵. روش نقطهٔ رأس (Corner Point Method)

برای حل LPهای دوبعدی روی کاغذ:

1. خطوط قیود را رسم کن  
2. سمت شدنی (feasible side) را مشخص کن  
3. نقاط تقاطع (گوشه‌ها) را پیدا کن  
4. نقاط غیرشدنی را حذف کن  
5. تابع هدف را در هر گوشه حساب کن  
6. بهترین مقدار را انتخاب کن  

---

## ۵.۱ قضیهٔ مهم

**اگر یک جواب بهینه وجود داشته باشد، حتماً در یکی از رأس‌های ناحیهٔ شدنی است.**

---

# ۶. انواع جواب‌ها در LP

---

## ۶.۱ جواب کران‌دار (Bounded)

ناحیهٔ شدنی محدود است → جواب بهینه وجود دارد.

---

## ۶.۲ جواب نامحدود (Unbounded)

وقتی تابع هدف می‌تواند بدون کران بهتر شود.

مثال:

تابع هدف:

$$
\min x
$$

قیود:

$$
x \ge 0,\quad y \ge 0
$$

می‌تواند تا بی‌نهایت کوچک شود → نامحدود.

---

## ۶.۳ جواب ناسازگار (Infeasible)

هیچ نقطه‌ای همهٔ قیود را ارضا نمی‌کند.

مثال:

$$
x \ge 5,\quad x \le 2
$$

---

## ۶.۴ بی‌نهایت جواب بهینه

وقتی تابع هدف با یک لبهٔ ناحیهٔ شدنی **موازی** است.

مثال:

تابع هدف:

$$
\min(x + y)
$$

قید:

$$
x + y = 10
$$

→ همهٔ نقاط روی این لبه بهینه‌اند.

---

# ۷. مثال LP (مشکل رژیم غذایی)

فرض کن:

$$
x = \text{تعداد سیب},\quad y = \text{تعداد موز}
$$

تابع هدف:

$$
\min(2x + y)
$$

قیود:

$$
\begin{aligned}
4x + 2y &\ge 20 \\
x + 2y &\ge 15 \\
x, y &\ge 0
\end{aligned}
$$

---

# ۸. تمرین LP

متغیرها:

$$
x = \text{جعبهٔ کوچک},\quad y = \text{جعبهٔ بزرگ}
$$

تابع هدف:

$$
\min(2x + 5y)
$$

قیود:

$$
\begin{aligned}
x + y &\ge 10 \\
2x + 5y &\le 40 \\
x, y &\ge 0
\end{aligned}
$$

---

# ۹. خلاصهٔ مهم (Cheat Sheet)

### یک LP باید این‌طور باشد:
- تابع هدف خطی  
- قیود خطی  
- متغیرها غیرمنفی (در فرم استاندارد)

### روش حل دستی:
- رسم قیود  
- محاسبهٔ نقاط تقاطع  
- بررسی شدنی بودن  
- ارزیابی تابع هدف  
- انتخاب بهترین  

### سه حالت خاص:
- نامحدود  
- ناسازگار  
- جواب بی‌نهایت  


