---
title:  adversarial search, midterm
description: adversarial search, midterm
---


# 🚀 **WEEK 7 — ADVERSARIAL SEARCH (Deep Explanation)**

_(Minimax • Alpha-Beta • Expectimax)_

Adversarial search is used when you are not the only decision maker.  
There are opponents.  
Opponents limit your success.  
Thus normal search (like BFS/UCS/A*) is not enough.

Let’s go deeper section by section.

---

# ⭐ PART 1 — What is a Game Tree?

A **game tree** models a turn-based game as a structure:

- Nodes = game states
    
- Edges = moves
    
- Levels alternate between MAX and MIN
    
- Leaves = terminal states with scores (utilities)
    

Examples: chess, checkers, tic-tac-toe, Pacman vs ghost

Here is the structure:

```
MAX level
    ↓ choose best move
MIN level
    ↓ opponent chooses worst for you
MAX level
    ↓ …
Leaf level → utility numbers
```

---

# ⭐ PART 2 — Utility Values (DEEP Explanation)

Utilities are numerical outcomes that represent the desirability of a state.

Examples:

### Simple games:

- Win = +1
    
- Draw = 0
    
- Lose = -1
    

### Pacman examples (CS188 style):

- More food eaten → higher score
    
- Closer to ghost (when ghost is scared) → higher score
    
- Running into a ghost → very low utility
    

Utilities must have these properties:

### ✔ Comparable

MAX always prefers **higher** utility.  
MIN always prefers **lower** utility.

### ✔ Deterministic

Utility of a leaf does NOT depend on the path you took to get there.

---

# ⭐ PART 3 — MINIMAX (Deep Intuition)

Minimax solves this:

> “If I assume my opponent plays optimally against me, what move guarantees the **best worst-case outcome**?”

Why worst-case?

Because MIN is **hostile**.  
MIN is not random.  
MIN is not stupid.  
MIN is _perfectly trying to minimize your result_.

### Levels in Minimax:

- MAX levels → choose **max** child value
    
- MIN levels → choose **min** child value
    
- Leafs → fixed utilities
    

---

## 🔥 Complete Minimax Mathematical Definition

### Terminal node:

$$  
V(n) = U(n)  
$$

### MAX node:

$$  
V(n) = \max_{s \in Succ(n)} V(s)  
$$

### MIN node:

$$  
V(n) = \min_{s \in Succ(n)} V(s)  
$$

Final output of minimax is:

- Best guaranteed outcome
    
- Best move that ensures this
    

---

# ⭐ DEEP INTUITION: WHY MINIMAX WORKS

### Suppose MAX has two options:

- Move A leads to utilities: {+5, +10} depending on MIN’s play
    
- Move B leads to utilities: {−2, +100}
    

If MAX is rational & cautious:

### Move A worst-case = +5

### Move B worst-case = −2

Even though B can give +100,  
an optimal MIN will choose the bad outcome −2.

So Move A is better.

That’s exactly what minimax computes.

---

# ⭐ PART 4 — Minimax Complexity (Why it’s expensive)

Game tree depth = (m)  
Branching factor = (b)

Number of nodes:

$$  
O(b^m)  
$$

This grows HUGE even for small games:

- Chess: (b ≈ 35)
    
- Depth 10 means: ( 35^{10} \approx 2.7 \times 10^{15} ) states
    

This is why **alpha-beta pruning** was invented.

---

# ⭐ PART 5 — Alpha-Beta Pruning (Deep Explanation)

Alpha-beta does NOT change the answer of minimax.  
It changes only HOW MUCH tree we search.

Idea:

### Don’t explore branches that cannot possibly affect the final decision.

We maintain two values:

---

## 🔵 α (Alpha)

- Best value MAX has seen on its path so far
    
- Lower bound on possible outcome
    
- Initialized as:  
    $$  
    \alpha = -\infty  
    $$
    

At MAX nodes, α increases.

---

## 🔵 β (Beta)

- Best value MIN has seen on its path so far
    
- Upper bound on possible outcome for MAX
    
- Initialized as:  
    $$  
    \beta = +\infty  
    $$
    

At MIN nodes, β decreases.

---

# ⭐ THE KEY PRUNING RULES (very important)

### At a MAX node:

If child value ≥ β → **PRUNE**  
Why?  
MIN already has a better (lower) option elsewhere, so it will never allow MAX to reach this branch.

---

### At a MIN node:

If child value ≤ α → **PRUNE**  
Why?  
MAX already has a better (higher) option elsewhere, so will never let MIN go here.

---

# ⭐ Deep intuition for pruning

### Imagine this:

MIN is choosing between two branches A and B.

You start exploring B.

While exploring B, MIN already was promised a value of +3 from branch A.

Now during exploring B you find a child with value +5.

MIN thinks:

> “+5 is worse for me than +3.  
> I will never pick +5, because I already have +3.  
> So stop exploring here.”

This is **β pruning**.

---

# ⭐ Alpha-Beta Best Case Complexity

Best case occurs when the tree is ordered perfectly with best moves first.

Then complexity becomes:

$$  
O(b^{m/2})  
$$

This doubles the depth we can search.

This is HUGE in games like chess.

Worst case: same as minimax (no improvement).

---

# ⭐ PART 6 — Expectimax (Deep Explanation)

Expectimax is used **when opponent is stochastic**.

Examples:

- Pacman ghosts in CS188 who move randomly
    
- Dice games
    
- Games where actions have probabilities
    

In these games:

- Opponent DOES NOT minimize your result
    
- Opponent DOES NOT maximize your result
    
- Opponent behaves RANDOMLY (known probability distribution)
    

So instead of MIN nodes we have **CHANCE nodes**.

---

# 🔵 Expectimax Formula (very important)

$$  
V(n) = \sum_{s \in Succ(n)} P(s) \cdot V(s)  
$$

Meaning:

> Expected value = weighted sum of children according to probability.

### Key differences from minimax:

- No “max of mins”
    
- No worst-case
    
- No best-case
    
- Just _expected utility_
    

Thus:

- No guarantees
    
- No pruning using alpha-beta
    
- Agents behave optimally only in **expected utility** sense
    

---

# ⭐ PART 7 — Differences Between Minimax and Expectimax (deep)

|Aspect|Minimax|Expectimax|
|---|---|---|
|Opponent type|Rational adversary|Random / stochastic|
|Node type|MAX, MIN|MAX, CHANCE|
|Calculation|min/max of children|expectation|
|Guarantees|Worst-case optimal|Best expected outcome|
|Pruning|Alpha-Beta applies|Alpha-Beta NOT applicable|

This difference is **one of the most tested concepts**.

---

# ⭐ PART 8 — How to Solve Exam Problems (MINIMAX)

You must:

1. Start from leaves
    
2. Assign utility values
    
3. Move upward computing min/max
    
4. Write final value at root
    
5. Choose branch that corresponds to root’s final value
    

---

# ⭐ PART 9 — How to Solve Alpha-Beta Pruning Problems

Given a tree with left-to-right child order:

1. Track α and β values at each node
    
2. Update α at MAX nodes
    
3. Update β at MIN nodes
    
4. When prune condition is hit:
    
    - MAX: (v \ge β) → prune
        
    - MIN: (v ≤ α) → prune
        
5. Mark pruned branches
    

---

# ⭐ PART 10 — How to Solve Expectimax Problems

1. Compute leaf utilities
    
2. At chance nodes, compute weighted average
    
3. At MAX nodes, take max
    
4. Move upward
    

Example:

If a chance node has children:

- Value 8 with probability 0.5
    
- Value 2 with probability 0.5
    

Then:

$$  
V = 0.5 \cdot 8 + 0.5 \cdot 2 = 5  
$$

---

# 🎯 FULL DEEP SUMMARY (for your exam)

### MINIMAX:

- Perfect adversary
    
- Worst-case decision
    
- Uses min/max
    
- Optimal play guaranteed
    
- Time: (O(b^m))
    

### ALPHA-BETA:

- Same result as minimax
    
- Prunes impossible branches
    
- Best case: (O(b^{m/2}))
    
- Huge speedup
    
- Does NOT change values
    

### EXPECTIMAX:

- Opponent is random
    
- Uses expected values
    
- No min nodes
    
- No alpha-beta pruning
    
- No worst-case guarantee
    

---
# 🚀 **هفته ۷ — جستجوی خصمانه (Adversarial Search)**

### _(Minimax • Alpha-Beta • Expectimax — توضیح عمیق و کامل)_

در جستجوی معمولی، عامل تنها تصمیم‌گیرنده است.  
اما در بسیاری از مسائل، عامل با **حریف** مواجه است.  
این حریف مانع موفقیت او می‌شود.  
پس الگوریتم‌هایی مانند BFS/UCS/A* کافی نیستند.

در این بخش با سه الگوریتم بسیار مهم آشنا می‌شویم:

- Minimax
    
- Alpha-Beta Pruning
    
- Expectimax
    

---

# ⭐ **بخش ۱ — درخت بازی (Game Tree) چیست؟**

درخت بازی مدل‌سازی یک بازی دو نفره است:

- **گره‌ها** = حالت‌های بازی
    
- **یال‌ها** = حرکت‌ها
    
- **سطوح** به‌صورت MAX / MIN یکی‌درمیان هستند
    
- **برگ‌ها** = حالت‌های نهایی با یک مقدار سود (Utility)
    

مثلاً:

- شطرنج
    
- XO
    
- Pacman vs Ghost
    

ساختار کلی:

```
MAX level
   ↓ بهترین حرکت برای MAX
MIN level
   ↓ بهترین حرکت برای MIN (بدترین برای MAX)
MAX level
   ...
Leaf level → Utility
```

---

# ⭐ **بخش ۲ — مقدار سود (Utility) چیست؟**

مقدار سود یک عدد است که کیفیت یک حالت را بیان می‌کند.

مثال‌های ساده:

- برد = +1
    
- مساوی = 0
    
- باخت = -1
    

مثال Pacman (در CS188):

- تعداد غذاهای باقی‌مانده
    
- فاصله از ارواح
    
- امتیاز بازی
    

Utility باید:

### ✔ قابل مقایسه باشد

MAX مقدارهای بیشتر را دوست دارد.  
MIN مقدارهای کمتر را.

### ✔ قطعی باشد

همان leaf همیشه همان مقدار را دارد.

---

# ⭐ **بخش ۳ — الگوریتم Minimax (توضیح عمیق)**

Minimax دنبال پاسخ این سؤال است:

> «اگر فرض کنم حریفم کاملاً هوشمند و خصمانه است، چه حرکتی بهترین نتیجهٔ **بدترین حالت ممکن** را برای من تضمین می‌کند؟»

درخت شامل:

- گره‌های **MAX** → انتخاب بیشترین سود
    
- گره‌های **MIN** → انتخاب کمترین سود
    
- برگ‌ها → دارای مقدار ثابت
    

---

## 🔥 تعریف ریاضی Minimax

### اگر گره نهایی باشد:

$$  
V(n) = U(n)  
$$

### اگر گره MAX باشد:

$$  
V(n) = \max_{s \in Succ(n)} V(s)  
$$

### اگر گره MIN باشد:

$$  
V(n) = \min_{s \in Succ(n)} V(s)  
$$

---

# ⭐ **مفهوم عمیق Minimax**

فرض کن دو حرکت داری:

### حرکت A:

برگ‌ها → {5+, 10+}  
حداقل نتیجه = **+5**

### حرکت B:

برگ‌ها → {−2، +100}  
حداقل نتیجه = **−2**

حرکت A بهتر است، چون MIN همیشه بدترین حالت را برای MAX انتخاب می‌کند.

Minimax **همین منطق بدترین‌حالت** را به‌طور کامل محاسبه می‌کند.

---

# ⭐ **پیچیدگی زمانی Minimax (چرا خیلی کند است؟)**

اگر:

- (b) = ضریب انشعاب
    
- (m) = عمق درخت
    

تعداد کل گره‌ها:

$$  
O(b^m)  
$$

مثلاً در شطرنج:

- (b \approx 35)
    
- عمق ۱۰ → عددی حدود (35^{10})
    

وحشتناک بزرگ!

این دلیل وجود **Alpha-Beta** است.

---

# ⭐ **بخش ۴ — هرس Alpha-Beta (توضیح خیلی مهم و عمیق)**

Alpha-Beta مقدار **Minimax را تغییر نمی‌دهد**.  
فقط **سریع‌تر** آن را محاسبه می‌کند.  
چون شاخه‌هایی که **هرگز انتخاب نخواهند شد** را هرس می‌کند.

دو مقدار نگه می‌داریم:

---

## 🔵 α (آلفا)

- بهترین مقدار ممکن برای MAX تاکنون
    
- کران پایین برای MAX
    
- مقدار اولیه:  
    $$  
    \alpha = -\infty  
    $$
    

در گره‌های MAX مقدار α افزایش می‌یابد.

---

## 🔵 β (بتا)

- بهترین مقدار ممکن برای MIN تاکنون
    
- کران بالا برای MIN
    
- مقدار اولیه:  
    $$  
    \beta = +\infty  
    $$
    

در گره‌های MIN مقدار β کاهش می‌یابد.

---

# ⭐ **شرایط هرس (Pruning Conditions)**

### 🔥 در گره MAX:

اگر مقدار فرزند ≥ β  
→ **هرس**

چرا؟

MIN جای دیگری گزینهٔ بهتری (کمتر) دارد، پس اجازه نمی‌دهد MAX این شاخه را طی کند.

---

### 🔥 در گره MIN:

اگر مقدار فرزند ≤ α  
→ **هرس**

چرا؟

MAX جای دیگری گزینهٔ بهتری (بیشتر) دارد، پس دنبال این شاخه نمی‌رود.

---

# ⭐ **مفهوم عمیق Alpha-Beta**

مثال:

MIN بین دو شاخه A و B انتخاب می‌کند.

در شاخه A → بهترین مقدار = +3  
در شاخه B → هنگام بررسی به مقدار +5 می‌رسیم.

MIN فکر می‌کند:

> «+5 بدتر از +3 است.  
> پس هیچ‌وقت شاخه B را انتخاب نمی‌کنم.  
> ادامهٔ این شاخه بیهوده است → هرس.»

---

# ⭐ **پیچیدگی Alpha-Beta**

### بهترین حالت (ترتیب عالی بچه‌ها):

$$  
O(b^{m/2})  
$$

یعنی عمق مؤثر جستجو **دو برابر** می‌شود.

### بدترین حالت:

$$  
O(b^m)  
$$

مثل Minimax.

---

# ⭐ **بخش ۵ — الگوریتم Expectimax (توضیح خیلی مهم)**

Expectimax زمانی استفاده می‌شود که **حریف تصادفی** باشد:

- ارواح Pacman
    
- بازی‌های دارای تاس
    
- ربات‌ها یا عامل‌هایی با رفتار تصادفی
    

در این حالت MIN وجود ندارد.  
به‌جای آن **گره‌های شانس (Chance nodes)** داریم.

---

## 🔵 فرمول Expectimax:

$$  
V(n) = \sum_{s \in Succ(n)} P(s),V(s)  
$$

معنی:

> «ارزش برابر است با امید ریاضی خروجی‌ها.»

هیچ «کمینه» یا «بیشینه» وجود ندارد.

---

# ⭐ **تفاوت‌های کلیدی Minimax vs Expectimax**

|ویژگی|Minimax|Expectimax|
|---|---|---|
|نوع حریف|کاملاً خصمانه|تصادفی|
|نوع گره‌ها|MAX و MIN|MAX و CHANCE|
|عمل انتخاب|min/max|امید ریاضی|
|تضمین|بدترین حالت|میانگین مورد انتظار|
|هرس|دارد (Alpha-Beta)|ندارد|

---

# ⭐ **بخش ۶ — چگونه مسائل Minimax را حل کنیم؟**

1. از برگ‌ها شروع کن
    
2. مقدارها را بالا ببر
    
3. در MAX → بیشترین
    
4. در MIN → کمترین
    
5. مقدار نهایی ریشه = انتخاب MAX
    

---

# ⭐ **بخش ۷ — چگونه مسائل Alpha-Beta را حل کنیم؟**

1. α = −∞ ، β = +∞
    
2. در MAX → α را به‌روزرسانی کن
    
3. در MIN → β را به‌روزرسانی کن
    
4. اگر شرط هرس برقرار شد ← prune
    
5. شاخه‌های هرس‌شده را علامت بزن
    

این یکی از رایج‌ترین سوالات میان‌ترم CS188 است.

---

# ⭐ **بخش ۸ — چگونه مسائل Expectimax را حل کنیم؟**

1. مقدار برگ‌ها را بخوان
    
2. در گره CHANCE → مقدار امیدریاضی:  
    $$  
    V = \sum P_i \cdot V_i  
    $$
    
3. در MAX → بیشترین مقدار
    
4. مقدار را به ریشه منتقل کن
    

---

# 🎯 **خلاصهٔ عمیق هفته ۷**

### Minimax:

- حریف کاملاً خصمانه
    
- تصمیم‌گیری بدترین حالت
    
- min و max
    
- تضمین بهینه بودن
    
- زمان: (O(b^m))
    

### Alpha-Beta:

- همان نتیجهٔ Minimax
    
- بسیار سریع‌تر
    
- بهترین حالت: (O(b^{m/2}))
    
- هیچ تغییری در جواب ایجاد نمی‌کند
    

### Expectimax:

- حریف تصادفی
    
- استفاده از امیدریاضی
    
- بدون هرس
    
- مناسب Pacman و محیط‌های stochastic
    
