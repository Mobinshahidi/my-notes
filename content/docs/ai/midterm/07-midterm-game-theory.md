# 🚀 **WEEK 8 — GAME THEORY (Maximum Detail Version)**

Game theory studies **strategic interactions** between rational decision-makers.

In AI midterms (especially CS188-style), the focus is on **2-player normal-form games**.

Players choose actions simultaneously → outcome determined by a **payoff matrix**.

Let’s break everything deeply and intuitively.

---

# ⭐ PART 1 — GAME REPRESENTATION (PAYOFF MATRICES)

A normal-form game is written as a **matrix**, where:

- **Rows** = Player 1 strategies
    
- **Columns** = Player 2 strategies
    
- Each cell = a pair:  
    $$(u_1, u_2)$$  
    representing the payoff to Player 1 and Player 2
    

Example:

||C1|C2|
|---|---|---|
|**R1**|(3, 2)|(0, 1)|
|**R2**|(1, 4)|(2, 0)|

Interpretation:

- If Player 1 plays **R1** and Player 2 plays **C1**, the outcome is:
    
    - Player 1 gets **3**, Player 2 gets **2**.
        

Players choose their strategies **simultaneously**, knowing each other’s payoff structure.

---

# ⭐ PART 2 — BEST RESPONSES (DEEP EXPLANATION)

A strategy is a **best response** if it gives the maximum possible payoff given what the opponent does.

Example:

If opponent chooses C1:  
Player 1 compares:

- Payoff of R1 vs C1
    
- Payoff of R2 vs C1
    

Whichever gives more is the **best response**.

### Why important?

Because Nash equilibrium is defined using best responses.

---

# ⭐ PART 3 — STRICTLY DOMINATED STRATEGIES (VERY IMPORTANT)

A strategy is **strictly dominated** if there's another strategy that is **always better**, no matter what the opponent does.

Formally:

Strategy A is strictly dominated by B if:

$$  
u_1(B, c) > u_1(A, c) \quad \forall c  
$$

Meaning:

> “B is ALWAYS better than A.”

Strict domination tells us:

### ✔ Rational players NEVER play a strictly dominated strategy

### ✔ You can DELETE dominated strategies from the game

### ✔ This is the basis of the "iterative elimination" process

This is a big part of midterm questions.

---

## 🔥 Example of strictly dominated row

Suppose for Player 1:

- R1 gives payoffs: (1, 2)
    
- R2 gives payoffs: (3, 4)
    

Then:

$$  
3 > 1, \quad 4 > 2  
$$

So R2 **strictly dominates** R1.

Player 1 will NEVER play R1.  
We delete this row.

---

# ⭐ PART 4 — ITERATIVE ELIMINATION OF STRICTLY DOMINATED STRATEGIES

Sometimes domination only becomes visible AFTER you delete other dominated strategies.

### Process:

1. Find dominated rows → remove them
    
2. Find dominated columns → remove them
    
3. Repeat
    
4. Continue until no more dominated rows/columns remain
    

The resulting smaller matrix is called:

### 👉 **Reduced Game**

This often reveals Nash equilibria that were hidden.

---

# ⭐ PART 5 — PURE STRATEGY NASH EQUILIBRIUM (DETAILED)

A strategy pair ((a, b)) is a **pure Nash equilibrium** if:

- Given opponent plays b, player 1 cannot do better than a
    
- Given opponent plays a, player 2 cannot do better than b
    

Formally:

Player 1:  
$$  
u_1(a, b) \ge u_1(a', b) \quad \forall a'  
$$

Player 2:  
$$  
u_2(a, b) \ge u_2(a, b') \quad \forall b'  
$$

Interpretation:

> “Nobody would change their action if allowed to deviate unilaterally.”

### ✔ Stable outcome

### ✔ No regrets

---

# ⭐ HOW TO FIND PURE NASH (EXAM METHOD)

For Player 1 (rows):

- Circle the **highest payoff in each column**.
    

For Player 2 (columns):

- Circle the **highest payoff in each row**.
    

Any cell where **both** players' best responses appear is a **Nash equilibrium**.

This method appears in almost every game theory exam problem.

---

# ⭐ PART 6 — WHAT IF THERE IS NO PURE NASH EQUILIBRIUM?

Some games (like Rock-Paper-Scissors) have **no pure equilibrium**.

Reason:

- Each action is beaten by another
    
- So players keep switching
    
- No stable choice exists
    

These games require **mixed strategies**.

---

# ⭐ PART 7 — MIXED STRATEGY NASH EQUILIBRIUM (VERY IMPORTANT)

A mixed strategy is a **probability distribution** over actions.

Example:

Player 1 plays:

- R1 with probability (p)
    
- R2 with probability (1-p)
    

Player 2 plays:

- C1 with probability (q)
    
- C2 with probability (1-q)
    

---

## 🎯 **KEY IDEA (EXTREMELY IMPORTANT):**

In a mixed strategy equilibrium:

### The opponent must be _indifferent_ between the actions they randomize over.

Because if one action were strictly better, they would not randomize.

---

# ⭐ PART 8 — HOW TO COMPUTE MIXED STRATEGIES (FULL DETAIL)

Let’s say Player 2 must be indifferent between choosing C1 and C2.

Compute expected payoff to Player 2 from C1 and C2.

### Example

Payoff matrix for Player 2:

||C1|C2|
|---|---|---|
|R1|4|1|
|R2|2|3|

Player 1 mixes:

- (p) = probability of choosing R1
    
- (1 - p) = probability of choosing R2
    

### Expected payoff to Player 2:

For C1:

$$  
E(C1) = 4p + 2(1-p)  
$$

For C2:

$$  
E(C2) = 1p + 3(1-p)  
$$

### Set equal (indifference condition):

$$  
4p + 2(1-p) = p + 3(1-p)  
$$

Solve step-by-step:

Left:

$$  
4p + 2 - 2p = 2p + 2  
$$

Right:

$$  
p + 3 - 3p = -2p + 3  
$$

Set equal:

$$  
2p + 2 = -2p + 3  
$$

$$  
4p = 1  
$$

$$  
p = 0.25  
$$

Thus Player 1 plays:

- R1 with probability **0.25**
    
- R2 with probability **0.75**
    

Then compute Player 2’s mixing probability similarly.

---

# ⭐ PART 9 — WHY MIXING WORKS (INTUITION)

If Player 1 becomes predictable, Player 2 exploits them.

But if Player 1 randomizes optimally, Player 2 becomes **indifferent** between their actions and cannot exploit.

This is the fundamental idea behind:

- Optimal strategies
    
- Zero-sum games
    
- Many AI strategies
    

---

# ⭐ PART 10 — ZERO-SUM VS GENERAL-SUM GAMES

### Zero-sum:

- Player 1’s payoff = − Player 2’s payoff
    
- Poker, matching pennies
    
- Minimax fully applies
    

### General-sum:

- Payoffs are independent
    
- Nash equilibrium may involve cooperation or coordination

---
# 🚀 **هفتهٔ ۸ — نظریهٔ بازی‌ها (Game Theory) — نسخهٔ کاملاً مفهومی و عمیق**

نظریهٔ بازی‌ها مطالعهٔ **تصمیم‌گیری استراتژیک** بین چند عامل (بازیکن) است.  
برخلاف Minimax که فقط با یک حریف کاملاً خصمانه سروکار دارد، نظریهٔ بازی‌ها:

- رفتار چند بازیکن را همزمان تحلیل می‌کند
    
- انتخاب‌ها **به‌صورت همزمان** انجام می‌شوند
    
- هر بازیکن دنبال **بیشینه‌سازی سود خود** است
    
- تعادل‌ها (Equilibrium) و استراتژی‌ها تحلیل می‌شود
    

در درس AI و امتحان میان‌ترم، تمرکز روی نسخهٔ سادهٔ نظریهٔ بازی‌هاست:

✔ استراتژی‌های مغلوب (Dominated Strategies)  
✔ حذف ترتیبی آن‌ها (Iterative Elimination)  
✔ بازی کاهش‌یافته (Reduced Game)  
✔ تعادل نش خالص (Pure Nash Equilibrium)  
✔ تعادل نش آمیخته (Mixed-Strategy Nash Equilibrium)

حالا همه را کاملاً دقیق و روان توضیح می‌دهم.

---

# ⭐ **بخش ۱ — نمایش بازی (Payoff Matrix)**

بازی دونفره معمولاً به‌صورت یک ماتریس نمایش داده می‌شود:

- **سطرها = استراتژی‌های بازیکن ۱**
    
- **ستون‌ها = استراتژی‌های بازیکن ۲**
    
- هر خانه = یک زوج  
    $$(u_1, u_2)$$  
    که سود بازیکن ۱ و ۲ را نشان می‌دهد.
    

مثال:

||C1|C2|
|---|---|---|
|**R1**|(3, 2)|(0, 1)|
|**R2**|(1, 4)|(2, 0)|

مثلاً اگر Player 1 سطر اول (R1) را انتخاب کند و Player 2 ستون اول (C1) را:

- Player ۱ → سود **۳**
    
- Player ۲ → سود **۲**
    

حرکت‌ها **همزمان** انجام می‌شوند.

---

# ⭐ **بخش ۲ — پاسخ بهینه (Best Response)**

پاسخ بهینه یعنی بهترین انتخاب یک بازیکن با فرض اینکه انتخاب حریف مشخص است.

مثال:

اگر Player 2 ستون C1 را انتخاب کند، Player 1 نگاه می‌کند که در سطر R1 بهتر است یا R2؟  
بالاترین سود → بهترین پاسخ.

این مفهوم پایهٔ تعریف تعادل نش است.

---

# ⭐ **بخش ۳ — استراتژی‌های کاملاً مغلوب (Strictly Dominated Strategies)**

یک استراتژی **کاملاً مغلوب** است اگر یک استراتژی دیگر **همیشه** بهتر باشد،  
بدون توجه به اینکه حریف چه کاری انجام می‌دهد.

تعریف ریاضی:

اگر برای Player 1، استراتژی A توسط B مغلوب شود، یعنی:

$$  
u_1(B, c) > u_1(A, c) \quad \forall c  
$$

تفسیر:

> «B در هر حالت بهتر از A است.»

پس:

- بازیکن عقلانی **هرگز** A را انتخاب نمی‌کند.
    
- می‌توانیم A را **حذف کنیم**.
    

این یکی از **سؤال‌های تضمینی امتحان** است.

---

## 🔥 مثال ساده

اگر سود Player 1 چنین باشد:

||C1|C2|
|---|---|---|
|R1|1|2|
|R2|3|4|

چون در هر دو ستون:

- 3 > 1
    
- 4 > 2
    

پس R2 کاملاً R1 را مغلوب می‌کند و R1 حذف می‌شود.

---

# ⭐ **بخش ۴ — حذف ترتیبی استراتژی‌های مغلوب (Iterative Elimination)**

گاهی بعد از حذف یک استراتژی، استراتژی‌های جدیدی نیز مغلوب می‌شوند.

روش حذف ترتیبی:

1. استراتژی‌های کاملاً مغلوب Player 1 را حذف کن
    
2. سپس استراتژی‌های Player 2 را بررسی و حذف کن
    
3. دوباره Player 1 را بررسی کن
    
4. این روند را ادامه بده تا هیچ استراتژی مغلوبی نماند
    

نتیجهٔ نهایی = **بازی کاهش‌یافته (Reduced Game)**

امتحان‌ها معمولاً از شما می‌خواهند این فرآیند را کامل انجام دهید.

---

# ⭐ **بخش ۵ — تعادل نش خالص (Pure Nash Equilibrium)**

تعادل نش نقطه‌ای است که در آن **هیچ بازیکنی تمایلی برای تغییر یک‌طرفهٔ انتخاب خود ندارد**.

یعنی:

- اگر Player 2 بماند، Player 1 نمی‌تواند سود خود را با تغییر حرکت بهتر کند.
    
- اگر Player 1 بماند، Player 2 هم نمی‌تواند بهتر کند.
    

تعریف ریاضی:

برای Player 1:

$$  
u_1(a, b) \ge u_1(a', b) \quad \forall a'  
$$

برای Player 2:

$$  
u_2(a, b) \ge u_2(a, b') \quad \forall b'  
$$

### تفسیر:

> «هیچ‌کس پشیمان نیست.»

---

# ⭐ **روش سریع امتحانی برای پیدا کردن Nash خالص**

۱. برای Player ۱:  
در هر ستون، **بالاترین سود** را علامت بزن.

۲. برای Player ۲:  
در هر سطر، **بالاترین سود** را علامت بزن.

۳. خانه‌هایی که هر **دو علامت** را دارند → **تعادل نش خالص**

این روش ۹۰٪ مواقع در امتحان‌ها استفاده می‌شود.

---

# ⭐ **بخش ۶ — مواقعی که تعادل خالص وجود ندارد**

بعضی بازی‌ها (مثل سنگ-کاغذ-قیچی) هیچ تعادل Nash خالص ندارند.

چرا؟

- هر حرکت توسط حرکت دیگری شکست می‌خورد.
    
- هیچ حرکت «ثابت» وجود ندارد.
    
- بازیکنان مدام در حال عوض‌کردن انتخاب هستند.
    

در این حالت، به سراغ **تعادل آمیخته (Mixed Strategy Nash Equilibrium)** می‌رویم.

---

# ⭐ **بخش ۷ — تعادل نش آمیخته (Mixed Strategies) — توضیح عمیق**

در این حالت بازیکن‌ها **حرکت‌های خود را با احتمال** انتخاب می‌کنند.

برای Player 1:

- با احتمال (p) → R1
    
- با احتمال (1 - p) → R2
    

برای Player 2:

- با احتمال (q) → C1
    
- با احتمال (1 - q) → C2
    

---

## 🎯 ایدهٔ کلیدی (فوق‌العاده مهم):

در تعادل آمیخته، باید حریف **بین انتخاب‌هایش بی‌تفاوت شود**.

چرا؟

چون اگر یک انتخاب بهتر باشد، بازیکن به آن گرایش پیدا می‌کند  
و در نتیجه استراتژی تصادفی نامتعادل می‌شود.

پس در تعادل نش آمیخته:

- مقدار امیدریاضی استراتژی‌های Player 2 باید **برابر** باشد
    
- مقدار امیدریاضی استراتژی‌های Player 1 نیز **برابر** باشد
    

---

# ⭐ **بخش ۸ — محاسبهٔ تعادل نش آمیخته (گام به گام)**

مثال:

payoffهای Player 2:

||C1|C2|
|---|---|---|
|R1|4|1|
|R2|2|3|

فرض کنیم Player 1 با احتمال (p) سطر اول را انتخاب می‌کند.

### محاسبهٔ امیدریاضی Player 2 برای ستون اول:

$$  
E(C1) = 4p + 2(1-p)  
$$

برای ستون دوم:

$$  
E(C2) = 1p + 3(1-p)  
$$

برای بی‌تفاوت شدن Player 2:

$$  
E(C1) = E(C2)  
$$

یعنی:

$$  
4p + 2(1-p) = p + 3(1-p)  
$$

حل:

چپ:

$$  
4p + 2 - 2p = 2p + 2  
$$

راست:

$$  
p + 3 - 3p = -2p + 3  
$$

برابر:

$$  
2p + 2 = -2p + 3  
$$

$$  
4p = 1  
$$

$$  
p = 0.25  
$$

یعنی Player 1 باید:

- R1 را با احتمال **۰٫۲۵**
    
- R2 را با احتمال **۰٫۷۵**
    

انتخاب کند.

سپس با همین روش (q) را برای Player 2 به‌دست می‌آوریم.

---

# ⭐ **بخش ۹ — چرا استراتژی آمیخته جواب می‌دهد؟ (فهم عمیق)**

اگر بازیکن ۱ قابل پیش‌بینی باشد، بازیکن ۲ از این پیش‌بینی استفاده می‌کند و سود بیشتری می‌گیرد.

اما اگر بازیکن ۱ طبق یک **الگوی تصادفی ایده‌آل** رفتار کند:

- Player 2 دیگر هیچ حرکت بهتری ندارد
    
- Player 2 نمی‌تواند Player 1 را exploit کند
    
- سیستم به تعادل می‌رسد
    

این اساس بسیاری از الگوریتم‌های AI است.

---

# ⭐ **بخش ۱۰ — بازی‌های صفرمجموع (Zero-Sum) vs غیرصفرمجموع**

### صفرمجموع:

- سود Player 1 = زیان Player 2
    
- مثل بازی Matching Pennies
    
- تحلیل با Minimax همخوانی دارد
    

### غیرصفرمجموع:

- سودها مستقل از هم هستند
    
- ممکن است تعادل‌های همکاری‌محور شکل بگیرد
    

در امتحان‌ها معمولاً **غیرصفرمجموع ساده** می‌آید.
