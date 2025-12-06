---
title: states, midterm
description:  states, midterm

---

# 🌟 **WEEK 1 — State Spaces (Foundations of AI)**

This is the simplest topic **conceptually**, but it is also **one of the most frequently tested topics** on CS188 midterms.

Let’s start from zero.

---

# 1️⃣ What is a _State_ in AI?

A **state** = a complete description of the world at a given time **needed** to make a decision.

A good state representation must:

### ✔ Contain all information needed for future decisions

### ✔ Contain **no irrelevant information**

### ✔ Be the **smallest** representation that still preserves correctness

This is why exams ask:  
**“Give the smallest valid state space representation.”**

---

# 2️⃣ What is a _State Space_?

The **state space** = all possible states the agent can be in.

Example:  
Pacman on an N×M board  
→ state might be just: `(x, y)`  
→ state space size: `N × M`

But if Pacman must track **food eaten**, **ghosts**, **keys collected**, etc., the state must grow logically.

---

# 3️⃣ Minimal State Representation (VERY IMPORTANT FOR MIDTERM)

This is tested in multiple years—for example:

### ✔ CS188 Fall 2022 Q1, part (a), part (b) involves state-space reasoning

### ✔ CS188 Spring 2011 Q1 is **exactly** about giving a minimal state space

Example from the file:  
Pacman needs to eat 1 red pellet and 1 blue pellet.  
The official solution (page 1) states:  
State = **(x, y, eatenR, eatenB)**  

This is a perfect example.  
We do **not** track the number of pellets left.  
We only track whether Pacman _has eaten_ one of each → minimal.

---

# 4️⃣ How to Build a Minimal State Representation (Simple Recipe)

When you see a problem:

### Step 1: Identify what changes

- Position
    
- Collected items
    
- Remaining life/energy
    
- Direction
    
- Boolean achievements (eatenR, eatenB)
    

### Step 2: Ask: “What does the agent need to know to determine what happens next?”

If the information does NOT affect future decisions → **DO NOT include it.**

### Step 3: Convert to variables + domains

Example:

- x ∈ {1 … N}
    
- y ∈ {1 … M}
    
- eatenR ∈ {T, F}
    
- eatenB ∈ {T, F}
    

### Step 4: Multiply domain sizes → state space size

For the Pacman example:  
N × M × 2 × 2 = 4NM states  

---

# 🧠 5️⃣ THE EXAM LOVES THESE FOUR QUESTIONS

Every midterm year includes at least one:

### **A) Define the state representation**

### **B) What is the size of the state space?**

### **C) What is the branching factor (max successors)?**

### **D) What is the goal test?**

Let’s practice with examples from your PDFs.

---

# 💡 PRACTICE EXAMPLE 1 (from CS188 Spring 2011 Midterm)

Pacman eats 1 red + 1 blue pellet.  
**Question:** Give minimal state space.  
✔ Official Answer:  
State = (x, y, eatenR, eatenB)  

---

# 💡 PRACTICE EXAMPLE 2 (create a new one for you)

**A robot is exploring a maze. It must:**

- reach the goal
    
- avoid one ghost that moves randomly
    
- has battery B
    

**Your minimal state variables:**

1. robot position: (x, y)
    
2. ghost position: (gx, gy)
    
3. battery: b ∈ {0 … B}
    

**State space size:**  
N × M × N × M × (B+1)

---

# 🧩 Interactive Checkpoint (you answer)

### ❓ **Checkpoint 1:**

A vacuum robot is in a 5×5 grid. Dirt may or may not exist in each of the 25 squares.  
Robot can be in any of the 25 squares.  
Robot must clean all dirt.

👉 **Question:**  
What is the minimal state representation?  
(Hint: it requires position + dirt configuration)

Think before scrolling.

—

# ✔️ Correct Answer:

State =

- robot position: (x, y) ∈ {25 positions}
    
- dirt vector: a 25-bit binary vector indicating clean/dirty
    

State space size = 25 × 2²⁵

This kind of exponential dirt representation appears in classic AI examples.

---

# ✔️ What is the **branching factor**?

Branching factor = **maximum number of successors (children) a state can have**.

Equivalently:

> the maximum number of actions available from any state.

Examples:

- Grid world with 4 moves → branching factor = 4
    
- A problem where you choose a movement AND a radius r (0…R) → 5 × (R+1)

---

# 🎯 What You Must Remember for Exam (Mini Cheat Sheet)

### A state must:

- Be complete : **It must contain _all_ the information required to determine what actions are possible and what will happen next.**
    
- Be minimal
    
- Include variables whose change affects future actions
    
- Exclude anything irrelevant
    
### The state space size = product of domains.

### The branching factor = number of legal actions (sometimes affected by state). 

### The goal test checks the completion condition (e.g., eatenR=T AND eatenB=T).

---

# 🌟 **هفتهٔ ۱ — فضاهای حالت (State Spaces)**

_(مهم‌ترین پایهٔ کل درس)_

هفتهٔ ۱ اولین و بنیادی‌ترین بخش درس هوش مصنوعی است. اگر این بخش را خوب بفهمی، تمام موضوعات بعدی—جست‌وجو، CSP، مینیمکس، نظریه بازی، MAB، و حتی بهینه‌سازی—برات بسیار واضح و طبیعی خواهند شد.

بیایید از صفر و کاملاً اصولی شروع کنیم.

---

# ۱️⃣ **State چیست؟**

در هوش مصنوعی، **State یا حالت** یعنی:

> «حداقلی‌ترین توصیف کامل از وضعیت محیط در یک لحظه که برای تصمیم‌گیری لازم است.»

ویژگی‌های یک «State» خوب:

### ✔ باید **تمام اطلاعات لازم** برای تصمیم‌گیری آینده را داشته باشد

### ✔ باید **هیچ اطلاعات اضافی** نداشته باشد

### ✔ باید **حداقلی (Minimal)** باشد

به همین دلیل است که در امتحان همیشه سؤال می‌دهند:

**«کوچک‌ترین نمایش معتبر از فضای حالت را تعریف کنید.»**

---

# ۲️⃣ **State Space یا فضای حالت چیست؟**

فضای حالت = تمام حالت‌های ممکن.

مثلاً اگر پکمن در یک محیط N×M باشد:  
`State = (x, y)`  
بنابراین **N × M حالت ممکن** داریم.

اما اگر پکمن باید موارد زیر را هم بداند:

- آیا غذا خورده شده؟
    
- آیا کلید گرفته شده؟
    
- انرژی چقدر است؟
    

پس State بزرگ‌تر می‌شود.

---

# ۳️⃣ **چگونه یک State حداقلی بسازیم؟ (بسیار مهم برای امتحان)**

### ✔ مرحله ۱: فقط چیزهایی را وارد State کن که **تغییر می‌کنند**

مثل:

- موقعیت
    
- آیتم‌های جمع‌آوری‌شده
    
- مقدار انرژی
    
- جهت نگاه کردن
    
- وضعیت هدف‌ها (رسیده / نرسیده)
    

### ✔ مرحله ۲: اگر چیزی بر آینده اثر ندارد → **حذفش کن**

مثال: اگر فرقی ندارد پکمن ۱۰ غذای قرمز خورده یا ۱ غذا،  
فقط یک متغیر بولین کافی است:

`eatenRed = {T, F}`

### ✔ مرحله ۳: متغیرها و دامنهٔ آن‌ها را بنویس

مثلاً:

- x ∈ {1…N}
    
- y ∈ {1…M}
    
- eatenR ∈ {T, F}
    
- eatenB ∈ {T, F}
    

### ✔ مرحله ۴: اندازه فضای حالت = ضرب دامنه‌ها

مثال از فایل **Spring 2011**:  
  
State = (x, y, eatenR, eatenB)  
تعداد کل حالت‌ها = 4 × N × M

---

# ۴️⃣ **سؤالاتی که همیشه در Midterm از State Space می‌آید**

تقریباً هر سال، سؤالات زیر تکرار می‌شود:

### **A)** کوچک‌ترین نمایش state چیست؟

### **B)** اندازه فضای حالت چقدر است؟

### **C)** branching factor (حداکثر تعداد successorها) چقدر است؟

### **D)** goal test چیست؟

این‌ها پایهٔ تمام بخش‌های بعدی هستند.

---

# 📝 مثال واقعی امتحان (از فایل Spring 2011)

سؤال: پکمن باید یک غذا قرمز و یک غذا آبی بخورد.  
کوچک‌ترین State را بدهید.

✔ جواب رسمی در فایل:  
`(x, y, eatenR, eatenB)`  

---

# 🧠 مثال تمرینی ساخته‌شده برای تو

رباتی در یک محیط حرکت می‌کند و باید:

- به هدف برسد
    
- یک شبح تصادفی را دنبال کند
    
- باتری محدود B دارد
    

State =

- موقعیت ربات: (x, y)
    
- موقعیت شبح: (gx, gy)
    
- سطح باتری: b ∈ {0...B}
    

Space size =  
N × M × N × M × (B + 1)

---

# 🧩 سوال تعاملی (خودت جواب بده)

**سؤال:**  
جاروبرقی هوشمند در یک محیط ۵×۵ است.  
هر خانه ممکن است کثیف یا تمیز باشد (۲۵ خانه → ۲⁵² حالت).  
ربات در یکی از ۲۵ خانه است.

✔ چه State حداقلی لازم است؟

(فکر کن…)

### ✔ جواب صحیح:

State =

- موقعیت ربات: یکی از ۲۵ حالت
    
- وضعیت ۲۵ خانه: یک بردار ۲۵ تایی از {تمیز/کثیف}
    

پس فضای حالت =  
25 × 2²⁵

